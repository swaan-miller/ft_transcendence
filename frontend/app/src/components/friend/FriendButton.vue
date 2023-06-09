<template>
  <section>
    <button
      v-if="status == 'FRIEND'"
      class="unfriend"
      @click="unfriend(friend)"
    >
      Unfriend
    </button>
    <button
      v-if="status == 'PENDING'"
      class="pending"
      @click="cancelRequest(friend)"
    >
      cancel
    </button>
    <button
      v-if="status == 'NONE'"
      @click="sendUtilsFriendRequest(userStore.user.id, friend, friendStore)"
    >
      Add Friend
    </button>
  </section>
</template>

<script setup lang="ts">
import { ref, onBeforeMount } from "vue";
import { io } from "socket.io-client";
import { useFriendStore, type User } from "@/stores/FriendStore";
import { useUserStore } from "@/stores/UserStore";
import apiRequest, { baseUrl } from "@/utils/apiRequest";
import { sendUtilsFriendRequest, utilsUnfriend } from "./friendUtils";
const props = defineProps({
  friendId: Number,
});

const friendStore = useFriendStore();
const userStore = useUserStore();
const socket = io(baseUrl + "/friend");

const friend = ref();
const status = ref<string>("NONE");
const relation = ref();

onBeforeMount(async () => {
  await apiRequest(
    "/friend/relation/" + userStore.user.id + "/" + props.friendId,
    "get"
  )
    .then((response) => {
      status.value = response.data.status;
      relation.value = response.data;
    })
    .catch((error) => {
      console.error(error);
    });

  await apiRequest("/user/" + props.friendId, "get")
    .then((response) => {
      friend.value = response.data;
    })
    .catch((err) => {
      console.error(err);
    });

  socket.on("connect", () => {
    console.log(
      socket.id + " user",
      userStore.user.id,
      "connected to socket on player page"
    );
  });

  socket.on("friendRequest", async (data) => {
    if (data.source == userStore.user.id) {
      status.value = "PENDING";
    } else if (data.target == userStore.user.id) {
      await friendStore.updateUserList(userStore.user.id);
      status.value = "PENDING";
    }
  });

  socket.on("requestAccepted", async (data) => {
    if (data.source == userStore.user.id) {
      await friendStore.updateUserList(userStore.user.id);
      status.value = "FRIEND";
    }
  });

  socket.on("unfriend", async (data) => {
    if (data.target == userStore.user.id || data.source == userStore.user.id) {
      await friendStore.updateUserList(userStore.user.id);
      status.value = "NONE";
    }
  });
});

async function unfriend(player: User) {
  const user = friendStore.users.find((friend) => friend.id === player.id);

  if (user) {
    utilsUnfriend(user, friendStore);
  } else {
    const newUser = new UserDto();
    const relations = new RelationDto();
    newUser.avatarUrl = friend.value.avatarUrl;
    newUser.id = friend.value.id;
    newUser.playerName = friend.value.playerName;
    newUser.status = friend.value.status;
    relations.source = userStore.user.id;
    relations.target = friend.value.id;
    relations.status = "FRIEND";
    newUser.relation = relations;
    await friendStore.removeRelation(newUser);
    relations.source = friend.value.id;
    relations.target = userStore.user.id;
    newUser.relation = relations;
    await friendStore.removeRelation(newUser);
    status.value = "NONE";
  }
}

class RelationDto {
  source!: number;
  target!: number;
  status!: string;
}

class UserDto {
  id!: number;
  playerName!: string;
  status!: number;
  avatarUrl!: string | undefined;
  relation!: RelationDto;
}

async function cancelRequest(player: User) {
  const user = friendStore.users.find((friend) => friend.id === player.id);

  if (user) {
    await friendStore.removeRelation(user);
    if (user?.relation != undefined) {
      status.value = user?.relation.status;
    }
  } else {
    const newUser = new UserDto();
    const relations = new RelationDto();
    newUser.avatarUrl = friend.value.avatarUrl;
    newUser.id = friend.value.id;
    newUser.playerName = friend.value.playerName;
    newUser.status = friend.value.status;
    relations.source = userStore.user.id;
    relations.target = friend.value.id;
    relations.status = "PENDING";
    newUser.relation = relations;
    await friendStore.removeRelation(newUser);
    relations.source = friend.value.id;
    relations.target = userStore.user.id;
    newUser.relation = relations;
    await friendStore.removeRelation(newUser);
    status.value = "NONE";
  }
}
</script>
<style scoped>
.pending {
  background: #ff7200;
}

.pending button:hover,
button:active {
  background: #ff7200;
}

.unfriend {
  background: #ff1818;
}
</style>

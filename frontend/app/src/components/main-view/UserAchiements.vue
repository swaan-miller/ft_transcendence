<template>
  <div class="flex-container box-styling">
    <h2>Achievements</h2>
    <div class="achievement-container">
      <div v-for="achievement in achievements" :key="achievement.id">
        <font-awesome
          class="font-awesome"
          :style="[
            achievementEarned(achievement.id)
              ? { opacity: 1 }
              : { opacity: 0.1 },
          ]"
          :icon="achievement.icon"
        />
        <p
          class="achievement-text"
          :class="{ active: showDescription === achievement.id }"
        >
          {{ achievement.name }}
        </p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import apiRequest from "@/utils/apiRequest";
import {
  faPenToSquare,
  faGamepad,
  faTableTennisPaddleBall,
  faFileImage,
  faTrophy,
  faThumbsDown,
  faHelmetSafety,
  faMedal,
  faSadTear,
} from "@fortawesome/free-solid-svg-icons";
import { onBeforeMount, ref } from "vue";

type Achievement = {
  id: number;
  name: string;
  icon: string;
};

const props = defineProps({
  userId: { type: Number, required: true },
});

const chievs = ref<Array<Achievement>>();

onBeforeMount(async () => {
  await getAchievements();
});

const achievements = [
  { id: 0, icon: faFileImage, name: "Updated Avatar" },
  { id: 1, icon: faTrophy, name: "Won First Game" },
  { id: 2, icon: faThumbsDown, name: "Lost First Game" },
  { id: 3, icon: faHelmetSafety, name: "Enabled 2FA" },
  { id: 4, icon: faPenToSquare, name: "Updated Player Name" },
  { id: 5, icon: faGamepad, name: "Played First Game" },
  { id: 6, icon: faTableTennisPaddleBall, name: "Played 5 Games" },
  { id: 7, icon: faMedal, name: "Won 5 games" },
  { id: 8, icon: faSadTear, name: "Lost 5 games" },
];
function achievementEarned(id: number) {
  if (chievs.value) {
    if (chievs.value.find((achievement: Achievement) => achievement.id === id))
      return 1;
  }
  return 0;
}

async function getAchievements() {
  try {
    const res = await apiRequest(`/user/${props.userId}/achievements`, "get");
    if (res) chievs.value = res.data;
  } catch (error) {
    console.error(`Error in getAchievements(): ${error}`);
  }
}

const showDescription: number | null = null;
</script>

<style scoped>
.flex-container {
  display: flex;
  flex-direction: column;
  width: 375px;
  padding: 20px;
}
h2 {
  font-size: 50px;
  margin-bottom: 20px;
}
.achievement-container {
  position: relative;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  justify-items: center;
  align-items: center;
  row-gap: 20px;
}
.font-awesome {
  font-size: 75px;
  opacity: 0.1;
  margin: 0;
}
.achievement-text {
  position: absolute;
  display: none;
  background-color: grey;
  padding: 5px;
  border-radius: 5px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.3);
}
.font-awesome:hover + .achievement-text {
  display: block;
}
.font-awesome:hover + .achievement-text {
  display: block;
}
</style>

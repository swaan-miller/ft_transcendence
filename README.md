# ft_transcendence

![Vue.js](https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vuedotjs&logoColor=4FC08D)
![NestJS](https://img.shields.io/badge/nestjs-%23E0234E.svg?style=for-the-badge&logo=nestjs&logoColor=white)
![Typescript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

**Codam [42 Network] group project**: this full stack web application offers a real-time multiplayer Pong game with additional features such as chat functionality and a friends system that allows players to connect.

This project is a collaborative effort between [Michelle Jiam](https://github.com/MichelleJiam), [Niks Hariman](https://github.com/nhariman), [Nilo van Winden](https://github.com/nvanwinden), [Sanne Albreghs](https://github.com/salbregh) and [Swaan Miller](https://github.com/swaan-miller).

## Project requirements
- The backend must be written in **NestJS**.
- The frontend must be written in a **TypeScript** framework.
- The usage of a **PostgreSQL** database is required.
- The website must be a **single-page application** and the user should be able to use the **back** and **forward** buttons in the browser.
- The website should be **responsive** and offer the best user experience possible.
- Launch the application by a single call to `docker-compose up --build`.

**Security concerns**
- Any password stored in the database must be **hashed**.
- The website must be protected against **SQL injections**.
- Implement **server-side validation** for forms and any user input.

**User Account**
- The user must login using the **OAuth** system of 42 intranet.
- The user should be able to choose a **unique name**, **upload an avatar** and enable **two-factor authentication**.
- The user should be able to **add other users as friends** and see their **current status**.
- **Stats** have to be displayed on the user profile.
- Each user should have a **match history** including 1v1 games and a **ladder**. Anyone who is logged in should be able to consult it.

**Chat**
- The user should be able to create channels (chat rooms) that can be either **public**,
or **private**, or **protected** by a password.
- The user should be able to send **direct messages** to other users.
- The user should be able to **block** other users.
- The user who has created a new channel is automatically set as the **channel owner**
until they leave it. The channel owner can set a **password** required to access the channel, change
it, and also remove it. The channel owner is a **channel administrator**. They can set other users as
administrators. A user who is an administrator of a channel can **kick**, **ban** or **mute** (for a
limited time) other users, but not the channel owners.
- The user should be able to **invite other users to play a Pong game** through the chat
interface.
- The user should be able to **access other players profiles** through the chat interface.

**Game**
- Users should be able to play a live Pong game versus another player.
- There must be a **matchmaking system**: the user can join a queue until they get automatically matched with someone else.
- The game must be faithful to the original Pong (1972).
- You must offer some **customization options**.

### Login page
<img width="771" alt="Screen Shot 2023-03-23 at 4 40 55 PM" src="https://user-images.githubusercontent.com/58479085/227256681-16d71013-f52f-4be9-b8ef-0ec256b1bede.png">

### Homepage
<img width="1125" alt="Screen Shot 2023-03-23 at 4 42 24 PM" src="https://user-images.githubusercontent.com/58479085/227257140-d7d37a90-c673-4a9f-8cea-cca0d838e113.png">

### Account settings
<img width="600" alt="Screen Shot 2023-03-23 at 4 28 47 PM" src="https://user-images.githubusercontent.com/58479085/227253206-8f55f9e3-b7c8-4a5c-a133-c5055ba06748.png">

### 2FA
<img width="1202" alt="Screen Shot 2023-03-23 at 4 48 30 PM" src="https://user-images.githubusercontent.com/58479085/227259017-14608920-830d-4c6c-8cc8-9f602014a14a.png">

### Pong game
<img width="1314" alt="Screen Shot 2023-03-23 at 4 26 52 PM" src="https://user-images.githubusercontent.com/58479085/227252732-3ab1acf0-45cd-482e-9ae2-f495bd93dec8.png">

### User page
<img width="1108" alt="Screen Shot 2023-03-23 at 4 31 29 PM" src="https://user-images.githubusercontent.com/58479085/227253983-0f48315a-dde2-4ced-a627-b25a7ace5e6d.png">

### Leaderboard
<img width="1107" alt="Screen Shot 2023-03-23 at 4 36 43 PM" src="https://user-images.githubusercontent.com/58479085/227255529-924423ce-43e0-4bcf-a60d-84f2f7861724.png">

### Chat - dm's
<img width="1315" alt="Screen Shot 2023-03-23 at 4 20 51 PM" src="https://user-images.githubusercontent.com/58479085/227256518-3dcac4d2-1df8-487b-b892-e937c6cb82ab.png">

### Friends
<img width="1138" alt="Screenshot 2023-03-24 at 11 45 01" src="https://user-images.githubusercontent.com/58479085/227501637-553693fe-68d3-4483-9ef5-fb353c853bc7.png">

### Responsive menu
<img width="600" alt="Screenshot 2023-03-24 at 11 40 16" src="https://user-images.githubusercontent.com/58479085/227501976-db83da0c-8e87-44d6-ad7a-05b1d363fcba.png">


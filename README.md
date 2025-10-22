
<div align="center">

  <img src="https://firebasestorage.googleapis.com/v0/b/startup-e715a.firebasestorage.app/o/logo.png?alt=media&token=6610bca6-5edb-42f2-a8ff-6c35fb66d391" alt="Netrise Logo" width="200" />

  <h1>Netrise (Private Project)</h1>

  <p>
    A hyper-personalized digital advertising and campaign platform built on GCP and Firebase.
  </p>

  <p>
    <img alt="Tech" src="https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB">
    <img alt="Tech" src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white">
    <img alt="Tech" src="https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black">
    <img alt="Tech" src="https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white">
    <img alt="Tech" src="https://img.shields.io/badge/BigQuery-E670B2?style=for-the-badge&logo=bigquery&logoColor=white">
  </p>
  
</div>

<!-- <p align="center">
  <img src="URL_TO_YOUR_DEMO_GIF" alt="Netrise App Demo" width="800" />
</p> -->

## ## 💡 About The Project

Netrise is a full-stack, cloud-native mobile platform that connects companies and users through a smart, personalized campaign feed. It's built for scale using a modern, event-driven architecture on Google Cloud.

The goal is to deliver the *right content* to the *right user* at the *right time* by processing user signals (views, clicks, likes) to generate tailored recommendations.

---

## ## ✨ Core Features

| For Users | For Companies (Admin) |
| :--- | :--- |
| 👤 Interest-based profiling | 📈 Dashboard & Analytics |
| 🔥 Personalized campaign feed | 🎯 Targeted campaign creation |
| 🏆 Badges & Loyalty rewards | 🏙️ Targeting by city, age, & interest |
| ❤️ Likes, Bookmarks & Engagement | 🔔 Real-time notifications |

---

## ## 🚀 Tech Stack & Architecture

This project is built with a scalable, cloud-native tech stack.

<p align="center">
  <a href="https://reactnative.dev/">
    <img src="https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React Native">
  </a>
  <a href="https://nextjs.org/">
    <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white" alt="Next.js">
  </a>
  <a href="https://www.typescriptlang.org/">
    <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript">
  </a>
  <a href="https://firebase.google.com/">
    <img src="https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black" alt="Firebase">
  </a>
  <a href="https://cloud.google.com/">
    <img src="https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white" alt="Google Cloud">
  </a>
  <a href="https://cloud.google.com/bigquery">
    <img src="https://img.shields.io/badge/BigQuery-E670B2?style=for-the-badge&logo=bigquery&logoColor=white" alt="BigQuery">
  </a>
  <a href="https://cloud.google.com/run">
    <img src="https://img.shields.io/badge/Cloud_Run-2596be?style=for-the-badge&logo=googlecloud&logoColor=white" alt="Cloud Run">
  </a>
  <a href="https://www.nativewind.dev/">
    <img src="https://img.shields.io/badge/NativeWind-38bdf8?style=for-the-badge&logo=tailwindcss&logoColor=white" alt="NativeWind">
  </a>
</p>

| Area | Technologies |
| :--- | :--- |
| **Mobile App** | React Native, NativeWind/Tailwind, React Query |
| **Web Admin** | Next.js (App Router), Velzon (UI) |
| **Backend & Infra**| Firebase (Auth, Firestore), Cloud Functions (Gen2), Pub/Sub, Cloud Run |
| **Data Pipeline** | BigQuery, Dataform (SQLX), Firestore → BQ Extensions |

### System Architecture Flow

The recommendation engine is event-driven and runs on a decoupled architecture:

1.  **Event:** A new user signs up, triggering a 2nd Gen Firestore Cloud Function.
2.  **Queue:** The function publishes a message to a Pub/Sub topic.
3.  **Process:** A Cloud Run worker consumes the message.
4.  **Query:** The worker queries pre-computed BigQuery views (built by Dataform) to get recommendations.
5.  **Writeback:** The worker writes the final recommendations back to the user's document in Firestore.
6.  **Display:** The React Native app reads these recommendations in real-time.

---



## \#\# 📜 License

This project is proprietary and confidential.

-----
<div align="center"> <h3>Contact</h3> <p> <a href="https://www.google.com/search?q=https://www.linkedin.com/in/YOUR_USERNAME"> <img alt="LinkedIn" src="https://www.google.com/search?q=https://img.shields.io/badge/LinkedIn-0A66C2%3Fstyle%3Dfor-the-badge%26logo%3Dlinkedin%26logoColor%3Dwhite"> </a> <a href="https://twitter.com/YOUR_USERNAME"> <img alt="Twitter" src="https://www.google.com/search?q=https://img.shields.io/badge/Twitter-1DA1F2%3Fstyle%3Dfor-the-badge%26logo%3Dtwitter%26logoColor%3Dwhite"> </a> </p> </div>

```
```

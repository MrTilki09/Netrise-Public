<div align="center"><img src="URL_TO_YOUR_LOGO" alt="Netrise Logo" width="150" /><h1>Netrise</h1><p>A hyper-personalized digital advertising and campaign platform built on GCP and Firebase.</p><p><a href="https://github.com/YOUR_USERNAME/YOUR_REPO/actions"><img alt="Build Status" src="https://img.shields.io/github/actions/workflow/status/YOUR_USERNAME/YOUR_REPO/main.yml?branch=main&style=for-the-badge"></a><img alt="Framework" src="https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB"><img alt="Framework" src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white"><img alt="Platform" src="https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black"><img alt="Platform" src="https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white"><a href="https://github.com/YOUR_USERNAME/YOUR_REPO/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/github/license/YOUR_USERNAME/YOUR_REPO?style=for-the-badge&color=blue"></a></p></div>Netrise is a full-stack mobile advertising platform designed to deliver hyper-personalized campaign recommendations to users. It connects companies (advertisers) with end-users through a recommendation engine built on BigQuery, Dataform, and Cloud Run, all orchestrated within the Google Cloud ecosystem.## Core FeaturesFor Users: A personalized feed of campaigns, interest profiling, loyalty/badge systems, and engagement (likes/bookmarks).For Companies: A full admin panel to create and manage campaigns, with targeting based on city, user interests, and age.Recommendation Engine: A robust backend system that processes user signals (views, clicks, likes, bookmarks) with decay to generate tailored recommendations.Cold Start Handling: Provides global popular companies for new users and uses a company's score plus a freshness bonus for new campaigns.## Tech StackThis project is a full-stack, cloud-native application primarily using GCP and a JavaScript/TypeScript stack.AreaTechnologyPurposeMobile AppReact Native (CLI)Cross-platform (iOS/Android) user application.NativeWind/TailwindStyling and UI.React QueryServer state management and caching.FCM (Firebase)Push notifications for campaigns and activity.Web AdminNext.js 13+ (App Router)Admin dashboard for company campaign management.Velzon TemplateUI kit for the admin panel.Firestore Web SDKReal-time data sync for admin operations.Backend & InfraFirebase AuthUser authentication (Mobile/Web).FirestorePrimary application database (NoSQL).Cloud Functions (Gen2)Event-driven triggers (e.g., on user create).Pub/SubAsynchronous messaging queue for background tasks.Cloud RunServerless worker for consuming Pub/Sub messages and running recommendation logic.Data & MLBigQueryData warehouse for all raw and cleaned event data.Firestore to BQ ExtensionReal-time data export from Firestore to BigQuery.DataformSQLX-based ETL/ELT to build cleaned views and precomputed recommendation tables.## System Architecture & Data FlowThe recommendation engine is event-driven and runs on a decoupled architecture:User Creation: A new user signs up in the mobile app, creating a document in users/{uid} in Firestore.Event Trigger: A 2nd Gen Firestore trigger fires on...create and publishes a message (containing uid, city, etc.) to the bootstrap-requests-dev Pub/Sub topic.Async Processing: A Cloud Run worker, subscribed to the bootstrap-requests-dev topic, consumes this message.Recommendation Generation:The worker queries BigQuery for the user's profile segments (vw_user_profile_segments).It fetches precomputed candidate sets (e.g., precomputed_company_candidates, precomputed_campaign_candidates) which are refreshed by Dataform schedules.It applies MVP business logic (rule-based segmentation, activity filters, freshness bonuses).Writeback: The final list of recommended campaign/company IDs is written back to Firestore under the user's document (e.g., users/{uid}/recommended_campaigns).App Display: The React Native app listens to this Firestore document in real-time (or fetches via React Query) to display the personalized feed.## Recommendation Engine Deep DiveThe core of this project is its data modeling and scoring logic, built in BigQuery and Dataform.Key Signals & DecayUser interactions are weighted using exponential decay to prioritize recent activity.SignalDecay Half-life (τ)Click14 daysImpression10 daysDwell Time21 daysLike30 daysBookmark30 daysNot Interested30 daysCompany Popularity ScoreThe popular_companies table is a key input. A company's overall score is calculated as a weighted sum of various metrics:SQL/* Company Popularity Score Formula */
pop_score = 0.35*w_lb_ctr         /* Wilson Lower Bound CTR */
          + 0.15*ctr_bb           /* Beta-Bayesian CTR */
          + 0.15*dwell_norm       /* Normalized Dwell Time */
          + 0.12*like_rate_bb     /* Beta-Bayesian Like Rate */
          - 0.20*notint_rate_bb   /* Beta-Bayesian Not-Interested Rate */
          + 0.10*bookmark_rate_bb /* Beta-Bayesian Bookmark Rate */
          + 0.05*log(1+unique_clickers)
          + 0.08*novelty
Source: data_modeling.mdKey Data Models (BigQuery)cleaned_user_company_impressions: Deduplicates views within a 2-second window.cleaned_user_company_clicks: Captures dwell_seconds.feature_stats_daily: Stores daily pre-calculated stats like prior_ctr_30d.popular_companies: Main scoring table, windowed for 1, 7, and 30 days.cleaned_campaigns: Parses raw JSON changelogs into a structured table with active time windows (start_at, end_at).## Getting StartedPrerequisitesNode.js (v18+)Yarn or npmGCP Account with Firebase & BigQuery enabledFirebase CLI (npm install -g firebase-tools)Access to a development.json or .env file with service account keys.Project StructureBash.
├── /dataform/          # Dataform SQLX models and schedules
├── /mobile/            # React Native mobile app (users)
├── /web-admin/         # Next.js admin panel (companies)
├── /backend/
│   ├── /functions/     # Cloud Functions (Gen2) for triggers
│   └── /worker/        # Cloud Run worker (Dockerized)
└── ...
Installation & RunningClone the repository:Bashgit clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
Setup Mobile App:Bashcd mobile
npm install
# Add .env file with Firebase config
npx pod-install  # For iOS
npm run android  # Or npm run ios
Setup Web Admin:Bashcd web-admin
npm install
# Add .env.local file with Firebase config
npm run dev
Deploy Backend:Bashcd backend/functions
npm install
firebase deploy --only functions

cd backend/worker
# Build and deploy Docker image to Cloud Run
# (Requires gcloud CLI)
gcloud run deploy ...
## ContributingContributions are welcome! Please open an issue to discuss your ideas or submit a pull request with your changes.Fork the repositoryCreate your feature branch (git checkout -b feature/AmazingFeature)Commit your changes (git commit -m 'Add some AmazingFeature')Push to the branch (git push origin feature/AmazingFeature)Open a Pull Request## LicenseThis project is licensed under the MIT License - see the LICENSE file for details.

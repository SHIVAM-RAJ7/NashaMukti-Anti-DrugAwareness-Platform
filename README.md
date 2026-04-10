# NashaMukti: Anti-Drug Awareness Platform

> A multi-role Android application built to digitize and amplify India's **Nasha Mukt Bharat Abhiyan (NMBA)** — connecting Institutes, Volunteers, and Victims through technology to build a drug-free India.

---

## 📖 Abstract

The consumption of toxic substances such as cigarettes, alcohol, and drugs has become a slow poison for India's youth — causing uneven deaths, severe untreated diseases, and irreversible damage to families and communities. NashaMukti is a mobile platform that transforms passive awareness into active participation by connecting every stakeholder of the NMBA campaign — government bodies, grassroots volunteers, and affected individuals — under one unified digital ecosystem.

---

## ✨ Features

### 🔐 Authentication & Onboarding
- Animated **3-slide onboarding** flow with Lottie illustrations
- **Firebase Email/Password Authentication** — Sign Up & Log In
- **Interest selection** screen — personalize your feed (Music, Sports, Tech, Art, Fitness, Food)
- **Interactive map onboarding** — pin your location using Google Maps with real-time reverse geocoding (Geoapify API) to capture city, district, and state

### 🏠 Home Feed
- **Instagram-style awareness feed** powered by Firebase Storage
- Posts include author, image, caption, hashtags, likes, comments, date and time
- Images loaded efficiently via **Glide** with memory and disk caching
- **FeaturedActivity** — curated featured awareness posts in a dedicated scroll view

### 💼 Jobs & Volunteer Opportunities
- **Dual job listing system** — featured cards (horizontal) + detailed listings (vertical)
- Opportunities from real organizations: **NMBA, NCB, PMO, Navjeevan Rehab, Jagruti Rehab**
- Master-detail navigation — tap any job to see full details with an Apply button
- Post new job opportunities via **AddJobActivity** with organization dropdown (NMBA, NCB, PMO)

### 📊 Task Progress Tracker
- Track volunteer and victim activity tasks with a **donut pie chart** per task
- Dynamic **color-coded status indicators**:
  - 🟢 Green — 75%+ completed
  - 🟠 Orange — 50–74% completed
  - 🔴 Red — below 50% completed
- Powered by **MPAndroidChart v3.1.0**
- Sample tasks: Share 500 posts, Invite 10 friends, Attend 3 events, Organize an event

### 🎬 Mukt Reels
- **TikTok/Instagram Reels-style** vertical video feed
- Built with **ViewPager2** for smooth vertical swipe navigation
- 10 bundled awareness video clips stored as raw resources
- Videos auto-play and loop via `MediaPlayer` with aspect-ratio scaling

### 🤖 Mukti — In-App Chatbot
- Floating chatbot dialog accessible from every screen via **FloatingActionButton**
- Named **"Mukti"** — assists users in finding nearby NMBA events
- Chat UI with **separate bubble layouts** for user and bot messages
- Powered by `MessagesRecyclerAdapter` with `sentByUser` boolean routing

### 📸 Create Post
- Pick image from gallery → preview → upload to **Firebase Storage**
- Real-time **upload progress dialog** showing percentage completion
- Images stored with **UUID-generated filenames** to prevent collisions
- Add caption and hashtags before posting

### 🗺️ Location Intelligence
- Every post model (`Post_info`) carries **latitude and longitude** geo-tags
- Enables government dashboard to **visualize awareness density** across India
- Identifies low-reach regions for targeted campaign intervention

### 🔔 Notifications
- Dedicated Notification fragment accessible from bottom navigation

---

## 🏗️ Architecture

### Tri-Role User System

```
User
 ├── Institute / Organization
 │     ├── Local Dashboard
 │     ├── Upload Data
 │     ├── Manage Volunteers
 │     └── Abhiyan Updates
 │
 ├── Volunteer
 │     ├── Host Events
 │     ├── Build Communities
 │     ├── Apply for Volunteership
 │     └── Connect with Victims
 │
 └── Victim / Addicted User
       ├── Upcoming Events
       ├── Fun Activities (Gamified)
       ├── Request Counselling
       ├── Track Daily Activities
       └── Be a Testimonial
```

### Complete App Flow

```
SplashScreen (3s)
      ↓
OnboardingScreen (3 slides with Lottie animations)
      ↓
SignUp ←→ LogIn  (Firebase Auth)
      ↓ new user        ↓ existing user
SelectInterest        MainActivity
      ↓
MapsActivity (location pinning + reverse geocoding)
      ↓
MainActivity
      ├── Home Fragment         → Awareness Feed
      ├── Notification Fragment → Updates
      ├── activity_applications → Jobs + Tasks
      ├── CreatePost            → Upload to Firebase Storage
      └── Chatbot Dialog        → Mukti assistant
```

### Package Structure

```
com.example.mukt/
├── onboarding_splash/
│   ├── SplashScreen.java
│   ├── OnboardingScreen.java
│   ├── Onboarding1.java
│   ├── Onboarding2.java
│   └── Onboarding3.java
│
├── signup_login/
│   ├── SignUp.java
│   └── LogIn.java
│
├── signup_onboarding/
│   ├── SelectInterest.java
│   └── MapsActivity.java
│
├── MainActivity.java
├── Home.java
├── Notification.java
├── CreatePost.java
├── FeaturedActivity.java
├── Mukt_reels.java
├── activity_applications.java
├── Application_Fragment1.java
├── Application_Fragment2.java
├── AddJobActivity.java
│
├── Post.java / Post_info.java
├── PostAdapter.java
├── Task.java / TaskAdapter.java
├── Video.java / VideoAdapter.java
├── Message.java / MessagesRecyclerAdapter.java
├── JobClass1.java / JobAdapter1.java
├── JobClass2.java / JobAdapter2.java
└── Feature_model.java / FeatureAdapter.java
```

---

## 🛠️ Tech Stack

### Core
| Technology | Version | Purpose |
|---|---|---|
| Java | 1.8 | Primary programming language |
| Android Studio | — | IDE |
| Android SDK | API 21–32 | Min Android 5.0 (Lollipop) |
| Gradle | 7.1.3 | Build system |
| ViewBinding | — | Type-safe view access |

### Firebase
| Service | Version | Purpose |
|---|---|---|
| Firebase Authentication | 19.2.0 | User sign up & login |
| Firebase Realtime Database | 19.2.1 | Real-time data sync |
| Firebase Storage | 20.0.0 | Image uploads & hosting |

### Google
| Service | Version | Purpose |
|---|---|---|
| Google Maps SDK | 18.0.1 | Interactive map |
| Google Location Services | 17.0.0 | FusedLocationApi / GPS |
| Secrets Gradle Plugin | 2.0.0 | Secure API key management |

### Third-Party Libraries
| Library | Version | Purpose |
|---|---|---|
| Glide | 4.13.2 | Image loading & caching |
| Lottie | 3.6.1 | JSON-based animations |
| MPAndroidChart | 3.1.0 | Donut pie charts |
| CircleImageView | 3.1.0 | Circular profile images |

### External APIs
| API | Purpose |
|---|---|
| Geoapify Reverse Geocoding | Converts GPS coordinates → city, district, state |
| Google Maps API | Interactive hybrid map |

---

## 🚀 Project Setup

### Prerequisites
- Android Studio (Bumblebee or later)
- JDK 1.8+
- Android SDK API 21+
- A Google Maps API Key
- A Firebase project with Auth, Realtime Database, and Storage enabled

### Steps

**1. Clone the repository**
```bash
git clone https://github.com/SHIVAM-RAJ7/NashaMukti-Anti-DrugAwareness-Platform.git
cd NashaMukti-Anti-DrugAwareness-Platform
```

**2. Open in Android Studio**
- Open Android Studio
- Select **Open an existing project**
- Navigate to the cloned folder

**3. Configure API Keys**

Create a `local.properties` file in the root directory and add:
```
MAPS_API_KEY=YOUR_GOOGLE_MAPS_API_KEY
```

**4. Configure Firebase**
- Go to [Firebase Console](https://console.firebase.google.com)
- Create a new Android project with package name `com.example.mukt`
- Download `google-services.json` and place it in the `/app` directory
- Enable **Email/Password Authentication**
- Enable **Realtime Database**
- Enable **Storage**

**5. Build & Run**
```bash
./gradlew assembleDebug
```
Or simply click **Run** in Android Studio.

---

## 📂 Firebase Data Structure

### Realtime Database
```json
{
  "posts": {
    "postId": {
      "author": "string",
      "imagelink": "string (Firebase Storage URL)",
      "caption": "string",
      "like": "int",
      "comment": "int",
      "data": "string (date)",
      "time": "string"
    }
  },
  "users": {
    "userId": {
      "email": "string",
      "role": "string (Institute/Volunteer/Victim)",
      "city": "string",
      "district": "string",
      "state": "string",
      "latitude": "float",
      "longitude": "float"
    }
  }
}
```

### Firebase Storage
```
images/
  └── {UUID}.jpg   ← user uploaded post images
```

---

## 📋 Permissions

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.QUERY_ALL_PACKAGES" />
```

---

## 🗺️ Key Design Decisions

### Why Firebase Realtime Database?
Real-time sync is critical for a live community platform where volunteers and victims need instant event updates. Firebase handles authentication, storage, and database without requiring a separate backend server — ideal for rapid development.

### Why Geoapify over Google Geocoding?
Geoapify's reverse geocoding API provided city, district, and state data in a single call — district-level granularity was essential for the government's regional awareness monitoring dashboard.

### Why MPAndroidChart?
It's the most mature charting library available on Android via JitPack. The donut chart with configurable hole radius, color-coded segments, and disabled interaction gave us a clean progress indicator without custom drawing.

### Why raw resources for Reels videos?
Bundling videos as `res/raw` resources ensures they work fully offline — important for users in areas with poor connectivity, which often correlates with low awareness regions.

### Geo-tagged Posts (Post_info)
Every post carries latitude and longitude. This feeds into the data visualization layer, allowing the government to map awareness activity density across India and identify regions requiring targeted intervention.

---

## 🤝 Contributing

1. Fork the repository
2. Check open issues or create a new one for the feature/bug
3. Create your feature branch: `git checkout -b feature/YourFeature`
4. Commit your changes: `git commit -m 'Add YourFeature'`
5. Push to the branch: `git push origin feature/YourFeature`
6. Open a Pull Request

---

## 🔮 Future Improvements

- **Persistent login** — check `FirebaseAuth.getCurrentUser()` on splash to skip login for returning users
- **Save user interests** to Firebase after `SelectInterest`
- **Real NLP chatbot** — replace hardcoded Mukti responses with an actual backend
- **Live post feed** — replace hardcoded posts with Firebase Realtime Database listener
- **Role-based routing** — navigate to different dashboards based on user role after login
- **Fix threading bug** in `MapsActivity` — move UI updates to `runOnUiThread()`
- **Terms & Conditions enforcement** — validate CheckBox before allowing sign up
- **Government analytics dashboard** — aggregate `Post_info` geo-data into a regional heat map

---

## 📄 License

This project was developed for educational and social impact purposes under the Nasha Mukt Bharat Abhiyan initiative.

---

<p align="center">Built with ❤️ for a Drug-Free India 🇮🇳</p>



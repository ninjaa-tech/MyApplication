MyApplication – Dynamic Entity Dashboard

An Android application that demonstrates login authentication and dynamic entity loading using Retrofit, Gson, and Hilt.
The app supports multiple data schemas — for example, different keypasses will load different data structures (travel, mythology, etc.) and render them dynamically.

Features

User Login – authenticates with a POST request using username and student ID.

Dynamic Dashboard – fetches data via a GET request and displays it in a RecyclerView.

Schema-Aware Rendering – automatically adjusts displayed fields depending on the dataset.

Details Screen – shows full entity details when a dashboard item is tapped.

Hilt Dependency Injection – clean, scalable architecture.

Retrofit + Gson – for networking and flexible JSON parsing.

Requirements

Android Studio Giraffe (or newer)

Gradle 8.0+

Kotlin 1.9+

Minimum SDK: 28 (Android 9.0)

Target SDK: 34 (Android 14)

A device or emulator with internet access

Dependencies

These libraries are defined in libs.versions.toml for easy version management:

Library	Purpose
Retrofit 2.9.0	Networking (API calls)
Gson 2.10.1	JSON serialization/deserialization
Hilt 2.51	Dependency Injection
Material 1.12.0	UI components (Material Design)
RecyclerView	Displaying list of entities
Lifecycle KTX	ViewModel & LiveData helpers

In app/build.gradle.kts:

dependencies {
implementation(libs.androidx.core.ktx)
implementation(libs.androidx.appcompat)
implementation(libs.material)
implementation(libs.androidx.activity)
implementation(libs.androidx.constraintlayout)

    // Retrofit + Gson
    implementation(libs.retrofit.core)
    implementation(libs.retrofit.gson)
    implementation(libs.gson)

    // Hilt for DI
    implementation(libs.hilt.android)
    kapt(libs.hilt.compiler)

    // Lifecycle
    implementation(libs.lifecycle.viewmodel.ktx)
    implementation(libs.lifecycle.livedata.ktx)
}

Project Structure
MyApplication/
│
├── app/
│   ├── src/main/
│   │   ├── java/com/example/myapplication/
│   │   │   ├── ApiService.kt
│   │   │   ├── DashboardActivity.kt
│   │   │   ├── DetailsActivity.kt
│   │   │   ├── DynamicEntityAdapter.kt
│   │   │   ├── LoginRequest.kt
│   │   │   ├── LoginResponse.kt
│   │   │   ├── MainActivity.kt
│   │   │   ├── MyApp.kt
│   │   │   └── NetworkModule.kt
│   │   │
│   │   └── res/layout/
│   │       ├── activity_main.xml
│   │       ├── activity_dashboard.xml
│   │       ├── activity_details.xml
│   │       └── row_dynamic_entity.xml
│   │
│   ├── build.gradle.kts
│   └── proguard-rules.pro
│
├── gradle/
│   └── libs.versions.toml
│
├── settings.gradle.kts
├── build.gradle.kts
└── README.md

Setup Instructions
1. Clone the Repository
   git clone https://github.com/yourusername/MyApplication.git
   cd MyApplication

2. Open in Android Studio

Launch Android Studio

Select File > Open, then navigate to the project folder.

Wait for Gradle sync to complete.

3. Configure API Endpoints

The app uses two endpoints:

Login Endpoint:

POST /sydney/auth


Replace "sydney" with your class region (melbourne, perth, etc.).

Dashboard Endpoint:

GET /dashboard/{keypass}


Both are set in ApiService.kt:

@POST("sydney/auth")
fun login(@Body request: LoginRequest): Call<LoginResponse>

@GET("dashboard/{keypass}")
fun getDashboard(@Path("keypass") keypass: String): Call<ResponseBody>


If your backend uses different paths, update these accordingly.

4. Run the App

Select a device or emulator with internet access.

Click Run ▶ in Android Studio.

5. Login

Use:

Username: Your first name (e.g., Manish)

Password: Your student ID (e.g., 12345678)

If successful, you'll be redirected to the dashboard showing data for your assigned keypass.

Keypass Examples

Different logins fetch different datasets dynamically:

Keypass	Example Entities
travel	Destinations with country, bestSeason, etc.
mythology	Deities with just name
music	Songs and albums
students	User profiles
Common Issues
1. App Crashes After Login

Check Logcat for:

Expected BEGIN_ARRAY but was BEGIN_OBJECT


This means your JSON is wrapped in an object like:

{ "entities": [ ... ] }


The code already handles this, but verify your backend output.

2. Blank Dashboard

Ensure:

Your login credentials are correct.

keypass is included in the dashboard endpoint URL.

Network permissions are set:

<uses-permission android:name="android.permission.INTERNET" />


(Already included in AndroidManifest.xml.)

Building Release APK

Go to Build > Build Bundle(s)/APK(s) > Build APK(s).

The APK will be generated under:

app/build/outputs/apk/debug/app-debug.apk

Contributing

Fork the repository.

Create a new branch:

git checkout -b feature-name


Commit changes:

git commit -m "Add new feature"


Push and create a pull request.

License

This project is for educational purposes as part of Victoria University coursework.
Do not distribute outside of class assignments without permission.
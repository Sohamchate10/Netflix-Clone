# Netflix Clone iOS App (UIKit & Swift 5)

![Platform](https://img.shields.io/badge/platform-iOS-lightgrey.svg)
![Swift](https://img.shields.io/badge/Swift-5-orange.svg)
![UIKit](https://img.shields.io/badge/UI-UIKit-blue.svg)
![License](https://img.shields.io/badge/License-MIT-brightgreen.svg) <!-- Or choose appropriate license -->

## Overview

This repository contains the source code for a Netflix clone iOS application built programmatically using Swift 5 and UIKit. This project was developed as part of an educational iOS development course (originally taught by Amar, link below) demonstrating how to replicate core features and the user interface of the popular streaming service.

The primary goal is to showcase techniques for building a complex UI programmatically, integrating with external APIs, managing data persistence, and structuring an iOS application using common design patterns.

## Features

*   **Tab Bar Navigation:** Standard `UITabBarController` for navigating between Home, Coming Soon, Top Searches, and Downloads sections.
*   **Home Screen:**
    *   **Hero Header:** Dynamic prominent header view displaying a featured title with a gradient overlay.
    *   **Content Sections:** `UITableView` organizing content (Trending Movies, Popular, etc.).
    *   **Horizontal Scrolling Rows:** `UICollectionView` within table cells for horizontally browsing titles within categories.
    *   **Dynamic Navigation Bar:** Navigation bar animates on scroll (hides/appears) for better content visibility.
*   **Content Discovery:**
    *   **Coming Soon:** Dedicated tab listing upcoming titles (`UITableView`).
    *   **Search:** Integrated `UISearchController` allowing users to search for movies/TV shows via the TMDB API.
    *   **Search Results:** Displays search results (likely using a `UICollectionView`).
*   **Title Preview:**
    *   Navigate to a dedicated screen upon tapping a title.
    *   Displays title, overview, and an embedded `WKWebView`.
    *   Plays the official YouTube trailer fetched via the YouTube Data API.
*   **Download Functionality:**
    *   **Context Menu:** Long-press on a Home screen title reveals a "Download" option.
    *   **Core Data Persistence:** Saves metadata of downloaded titles locally.
    *   **Downloads Tab:** Fetches and displays downloaded titles from Core Data (`UITableView`).
    *   **Deletion:** Swipe-to-delete functionality in the Downloads tab.
    *   **Notification Center Updates:** Updates the Downloads tab instantly when a new title is downloaded elsewhere.
*   **API Integration:**
    *   **TMDB (The Movie Database):** Fetches movie/TV show metadata, posters, categories, and search results.
    *   **YouTube Data API v3:** Searches for and retrieves trailer video IDs.
*   **Asynchronous Image Loading:** Uses **SDWebImage** for efficient background image downloading and caching.
*   **Programmatic UI:** Entire user interface built using code (no Storyboards).
*   **Clean Architecture:** Attempts MVVM structure with distinct Model, View, and ViewModel components, plus Manager classes for services.

## Screenshots / Demo

*(**Placeholder:** You should replace this section with actual screenshots and ideally a GIF demonstrating the app's functionality, especially animations like the scrolling navigation bar and context menu.)*

**Example:**

| Home Screen                 | Title Preview              | Search Results             |
| :-------------------------- | :------------------------- | :------------------------- |
| ![Home Screen](link/to/home_screenshot.png) | ![Preview](link/to/preview_screenshot.png) | ![Search](link/to/search_screenshot.png) |

*Add a GIF link here showing navigation, scrolling, search, and trailer playback.*

## Technology Stack

*   **Language:** Swift 5
*   **UI Framework:** UIKit (Programmatic Auto Layout)
*   **Networking:** URLSession, JSONDecoder
*   **Concurrency:** Grand Central Dispatch (GCD)
*   **Data Persistence:** Core Data
*   **Image Loading:** SDWebImage
*   **Dependency Management:** Swift Package Manager (SPM)
*   **APIs:**
    *   The Movie Database (TMDB) API
    *   YouTube Data API v3
*   **Core Components:** `UITabBarController`, `UINavigationController`, `UIViewController`, `UITableView`, `UICollectionView`, `WKWebView`, `UISearchController`, `CAGradientLayer`, `NSNotificationCenter`.
*   **Design Patterns:** MVVM (intended), Singleton (for Managers), Delegate, Target-Action.

## Architecture

The project aims to follow the **Model-View-ViewModel (MVVM)** architecture pattern, although simplified for educational purposes.

*   **Models:** Structs representing data from APIs (e.g., `Title`, `YouTubeSearchResponse`) and Core Data entities (`TitleItem`).
*   **Views:** Custom `UIView`, `UITableViewCell`, `UICollectionViewCell` subclasses responsible for layout and presentation.
*   **ViewModels:** Structures (`TitleViewModel`, `TitlePreviewViewModel`) designed to prepare data specifically for display by the Views, decoupling them from the raw Models.
*   **Managers:** Singleton classes (`APICaller`, `DataPersistenceManager`) encapsulating logic for network requests and Core Data operations.
*   **Controllers:** `UIViewController` subclasses coordinating between Models, Views, and Managers.

## API Usage

This application relies on external APIs:

1.  **The Movie Database (TMDB):** Used for fetching all movie and TV show information. Requires an API key.
2.  **YouTube Data API v3:** Used for fetching trailer video IDs. Requires an API key enabled via Google Cloud Console.

**IMPORTANT:** You **must** obtain your own API keys from these services to run the application.

## Setup & Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/your-repo-name.git  <-- Replace with your repo URL
    cd your-repo-name
    ```
2.  **Open the project:** Open the `.xcodeproj` file in Xcode.
3.  **Configure API Keys:** See the section below.
4.  **Build and Run:** Select a target simulator or device and run the project (Cmd+R). Swift Package Manager should automatically resolve the SDWebImage dependency.

## Configuration - API Keys

You need to add your personal API keys for TMDB and YouTube for the app to function correctly.

1.  **Navigate** to the `Managers/APICaller.swift` file within the Xcode project.
2.  **Locate** the `Constants` struct inside the `APICaller` class.
3.  **Replace** the placeholder values for `API_KEY` and `YoutubeAPI_KEY` with your actual keys obtained from TMDB and Google Cloud Console, respectively.

```swift
// Inside Managers/APICaller.swift

class APICaller {
    static let shared = APICaller()

    struct Constants {
        static let API_KEY = "YOUR_TMDB_API_KEY_HERE" // <-- Replace this
        static let base_URL = "https://api.themoviedb.org"
        static let YoutubeAPI_KEY = "YOUR_YOUTUBE_API_KEY_HERE" // <-- Replace this
        static let YoutubeBase_URL = "https://youtube.googleapis.com/youtube/v3/search?"
    }

    // ... rest of the APICaller class
}
```

**⚠️ Warning:** Do **NOT** commit your API keys directly into your version control system (like Git). Consider using environment variables or a configuration file listed in your `.gitignore` for more secure key management in real applications.

## Potential Improvements & Future Work

*   Implement robust user-facing error handling (e.g., alerts).
*   Add loading indicators (e.g., `UIActivityIndicatorView` or skeleton views) during network requests.
*   Refactor network layer for less repetition (e.g., generic request function).
*   Prevent duplicate downloads in Core Data.
*   Implement actual background video file downloading.
*   Add Unit and UI Tests.
*   Improve Accessibility (VoiceOver labels, Dynamic Type support).
*   Explore more advanced state management (e.g., Combine).
*   Enhance ViewModel logic for better separation of concerns.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details (if applicable).

## Acknowledgements

*   Based on the iOS Development Course by **Amar** available on YouTube: [iOS Development Course - Use Swift 5 and UIKit to Build a Netflix Clone](https://www.youtube.com/watch/KCgYDCKqato)
```

**To Use This README:**

1.  **Save:** Copy the content above and save it as `README.md` in the root directory of your project.
2.  **Customize:**
    *   Replace the placeholder screenshot links with actual URLs to your screenshots/GIFs.
    *   Update the repository URL in the "Clone the repository" command.
    *   Choose and potentially add a `LICENSE.md` file if you haven't already.
3.  **Commit:** Add and commit the `README.md` file to your Git repository.

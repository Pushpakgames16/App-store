# Content Management System with Firebase

This project consists of two separate HTML files for managing and browsing content with Firebase integration.

## Files Overview

### `user.html` - Public Content Browser
- **Purpose**: For public users to browse, search, and rate content
- **Features**: 
  - Filter content by type (All, Games, Apps)
  - Search functionality
  - Star rating system
  - Modal popup for viewing content
  - Responsive design

### `admin.html` - Admin Panel
- **Purpose**: For site administrators to manage content
- **Features**:
  - Email/password authentication
  - Create, Read, Update, Delete (CRUD) operations
  - Form for adding/editing items
  - List view of all items with management options

## Firebase Data Structure

Both files interact with the same Firebase Realtime Database structure under the main node called `items`. Each item object must have the following keys:

```javascript
{
  "items": {
    "item_id_1": {
      "type": "games",           // "games" or "apps"
      "title": "Game Title",     // Display name
      "htmlCode": "https://...", // URL to embed/play
      "logoUrl": "https://...",  // Image URL for logo
      "avgRating": 4.2,         // Average rating (0-5)
      "totalRatings": 15,       // Number of ratings
      "sumOfRatings": 63        // Sum of all ratings
    },
    "item_id_2": {
      // ... same structure
    }
  }
}
```

## Setup Instructions

### 1. Firebase Configuration
1. Create a Firebase project at [Firebase Console](https://console.firebase.google.com/)
2. Enable Authentication (Email/Password)
3. Enable Realtime Database
4. Get your Firebase Web SDK configuration

### 2. Add Firebase SDK
Add the Firebase SDK to both HTML files by including these scripts before your custom JavaScript:

```html
<!-- Add these before your custom script tags -->
<script src="https://www.gstatic.com/firebasejs/9.x.x/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.x.x/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.x.x/firebase-database-compat.js"></script>
```

### 3. Configure Firebase
In both files, replace the placeholder configuration with your actual Firebase config:

```javascript
const firebaseConfig = {
  apiKey: "your-api-key",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project.firebaseio.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "your-app-id"
};
```

### 4. Database Rules
Set up your Firebase Realtime Database rules to allow read access for users and read/write for authenticated admins:

```json
{
  "rules": {
    "items": {
      ".read": true,
      ".write": "auth != null"
    }
  }
}
```

### 5. Authentication Setup
1. In Firebase Console, go to Authentication > Users
2. Add your admin user with email and password
3. Use these credentials to log into the admin panel

## Implementation Steps

### For `user.html`:
1. **Step 1**: Initialize Firebase with your config
2. **Step 2**: Implement Firebase listener to fetch items from `db.ref('items')`
3. **Step 3**: Implement rating system using Firebase transactions

### For `admin.html`:
1. **Step 1**: Initialize Firebase with your config
2. **Step 2**: Set up authentication state listener
3. **Step 3**: Implement login functionality
4. **Step 4**: Implement logout functionality
5. **Step 5**: Load items for management
6. **Step 6**: Implement form submission (Create/Update)
7. **Step 7**: Implement edit functionality
8. **Step 8**: Implement delete functionality

## Features

### Neon Theme Design
- Consistent neon color palette across both files
- Responsive design for mobile and desktop
- Smooth hover effects and transitions
- Modern UI with glassmorphism effects

### User Features (`user.html`)
- **Filtering**: Filter by content type (All, Games, Apps)
- **Search**: Real-time search through content titles
- **Rating**: Interactive star rating system with Firebase integration
- **Modal View**: Popup modal for viewing content in iframe
- **Responsive**: Works on all device sizes

### Admin Features (`admin.html`)
- **Authentication**: Secure login with email/password
- **CRUD Operations**: Full Create, Read, Update, Delete functionality
- **Form Management**: Add/edit form with validation
- **Item Management**: List view with edit/delete actions
- **Responsive**: Mobile-friendly admin interface

## Security Considerations

1. **Authentication**: Only authenticated users can access admin features
2. **Database Rules**: Configure Firebase rules to restrict write access
3. **Input Validation**: Validate all form inputs before saving
4. **Rate Limiting**: Consider implementing rate limiting for ratings

## Browser Compatibility

- Modern browsers (Chrome, Firefox, Safari, Edge)
- Requires JavaScript enabled
- Responsive design for mobile devices

## Customization

### Colors
The neon theme uses CSS variables that can be easily modified:
```css
:root {
  --neon-blue: #00ffff;
  --neon-pink: #ff00ff;
  --neon-green: #39ff14;
  --dark-bg: #0d0221;
  --light-bg: #261447;
  --text-color: #f0f0f0;
  --gold: #FFD700;
}
```

### Content Types
To add new content types, modify the filter buttons in `user.html` and the select options in `admin.html`.

## Troubleshooting

1. **Firebase not loading**: Check your Firebase configuration and SDK versions
2. **Authentication issues**: Verify your Firebase Authentication settings
3. **Database errors**: Check your Firebase Realtime Database rules
4. **CORS issues**: Ensure your Firebase project settings allow your domain

## Demo Mode

Both files include demo functionality that works without Firebase for testing the UI. Remove the demo code when implementing Firebase integration.
---
layout: post
title: Building a Music Player on web
date: 2024-12-26 13:20:51
tags: [React, SCSS, Video.js, AntDesign, Zustand, Material-UI]
categories: Web
---

Creating a web-based music player is an exciting project that combines modern web development tools and libraries. This application is inspired by the minimalist design of iOS, providing an intuitive interface for playing music and videos.

<!-- more -->

## Features

- **Responsive Design**: Built with CSS Grid and SCSS for consistent layouts across devices.
- **State Management**: Zustand efficiently handles player states like play, pause, and track changes.
- **Interactive Navigation**: Ant Design Tabs organize sections for easy browsing.
- **Advanced Video Playback**: Video.js powers smooth and customizable video experiences.
- **Rich UI Elements**: Material-UI ensures polished icons and buttons.

<div style="display: flex; justify-content: center; gap: 20px; align-items: stretch;">
  <img src="/images/musicPlayer/musicMoive.png" alt="Website Screenshot 1" style="width: 45%; height: auto; border-radius: 8px; object-fit: cover;">
  <img src="/images/musicPlayer/musicPlayer.png" alt="Website Screenshot 2" style="width: 45%; height: auto; border-radius: 8px; object-fit: cover;">
</div>

## Tools Used

- **React**: For building dynamic components.
- **SCSS**: To style and structure layouts.
- **Ant Design**: For elegant UI components.
- **Zustand**: Lightweight state management.
- **Video.js**: Advanced video support.
- **Material-UI**: Consistent design elements.

## Technique Points

Some specific coding techniques that I can share with you.

### **1. Using React Fragment**

- **Code**:

  ```jsx
  <React.Fragment key={index}>
  ```

  - `React.Fragment` is used to wrap multiple child elements without adding extra DOM nodes.
  - The `key` attribute is critical for React's performance optimization, allowing it to uniquely identify each child component during rendering.

### **2. Dynamic List Rendering**

- **Code**:

  ```jsx
  {songList.map((item, index) => (
    ...
  ))}
  ```

  - The `map` method is used to dynamically generate list items based on the `songList` data.
  - Each `item` in the list contains information about the song (e.g., image, title, singer, time), which is used to construct the corresponding UI.

### **3. Conditional Rendering**

- **Code**:

  ```jsx
  {isPlaying && currentSong === item ? (
    <PauseCircleOutlineIcon />
  ) : (
    <PlayCircleOutlineIcon />
  )}
  ```

  - Conditional rendering is used to dynamically display the play or pause icon based on the current state of the song.
  - If the current song is playing, a pause icon is displayed; otherwise, a play icon is shown.

### **4. State Management**

- **Code**:

  ```jsx
  onClick={() =>
    currentSong === item ? togglePlay() : setCurrentSong(item)
  }
  ```

  - `onClick` handles user interaction for each song in the list.
  - If the currently selected song is already playing, the `togglePlay` function is triggered to pause or play the song.
  - Otherwise, `setCurrentSong` updates the state to make the selected song the current song.

## Conclusion

This project combines modern tools to create a sleek and functional music player. Future improvements include playlist management and integration with streaming services.

## Explore the Project

- [View the Website Live](https://jzzzzskr.github.io/player/)
- [Check the Source Code on GitHub](https://github.com/JzzzzSkr/player)

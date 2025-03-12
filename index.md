---
layout: post
title: Digital Rain Animation in Modern C++
tags: cpp coding project terminal animation
categories: project
---

# Digital Rain Animation

This project creates a Matrix-style "digital rain" effect in the terminal using modern C++. The animation displays falling characters that mimic the iconic computer code rain seen in the Matrix films.

## Project Overview

The animation runs in any standard terminal and creates cascading blue characters that fall from the top of the screen to the bottom. When a character reaches the bottom, it wraps around to the top again, creating a continuous rain effect.

Assets/Rain.png

## Technical Components

The project uses several C++ features to create a clean, object-oriented implementation:

### Core Components

- **DigitalRain class** - Main class that handles the rain effect.
  Located in `DigitalRain.h` and implemented in `DigitalRain.cpp`

- **Vector** - Stores rain drop positions.
  `std::vector<int> columnPositions;` in the DigitalRain class

- **Enums** - Simple settings for speed and display style.
  `enum class Speed { Medium }; enum class Mode { Alternate };`

- **ANSI codes** - Makes colors and clears the screen.
  `std::cout << "\033[2J\033[H";` for clearing and `std::cout << "\033[94m" << ch << "\033[0m";` for colors

### Animation Techniques

- **Loop system** - Repeats update and display steps.
  `while (true) { render(); update(); std::this_thread::sleep_for(...); }`

- **Timing** - Controls animation speed.
  `std::this_thread::sleep_for(std::chrono::milliseconds(100));`

- **Random numbers** - Creates varied rain patterns.
  `columnPositions[i] = std::rand() % height;`

- **Wrap-around math** - Makes rain loop at screen bottom.
  `columnPositions[i] = (columnPositions[i] + 1) % height;`

### Visual Elements

- **ASCII art** - Uses "|" and ":" for rain drops.
  `ch = '|';` for heads and `ch = ':';` for tails

- **Position tracking** - Keeps rain drops moving properly.
  `if (row == columnPositions[col]) { /* display head */ }`

## Project Structure

The project is organized into three main files:

1. **DigitalRain.h** - Contains class declarations and enums
2. **DigitalRain.cpp** - Contains the implementation of the DigitalRain class
3. **main.cpp** - Creates and runs the DigitalRain object

<img src="https://raw.githubusercontent.com/DenisJ123/digital-rain-cpp/main/docs/assets/images/DigitalRainDev1.png" width="400" height="300">

## Implementation Details

The animation uses ANSI escape sequences to control the terminal display. These are special codes that tell the terminal to perform actions like clearing the screen or changing text color.

For example, this code clears the screen between animation frames:
```cpp
void DigitalRain::clearScreen() const {
    // ANSI escape sequence: clear screen and move cursor to top-left
    std::cout << "\033[2J\033[H";
}

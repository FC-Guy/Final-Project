# Daily Boost – Quotes & Mood Tracker

## Table of Contents
- Overview
- Product Spec
- Wireframes
- Schema

---

# Overview

## Description
Daily Boost is a simple mobile app that gives users one inspirational quote each day and lets them log their mood (happy / okay / sad). Users can save favorite quotes and view a small history of their moods over time. The goal is to help students and busy people get motivated quickly and build a positive daily habit.

---

## App Evaluation

**Category:** Lifestyle / Health & Wellness  
**Mobile:** Designed for quick mobile use; ideal for a once-a-day check-in.  
**Story:** “Open the app, get your quote, record your mood.” Simple and clear daily value.  
**Market:** Useful for students, young adults, and anyone who likes motivation or tracking how they feel.  
**Habit:** Encourages daily engagement by giving a new quote and mood logging each day.  
**Scope:** Narrow and easy to build. MVP includes 2 screens and a single API request.

---

# Product Spec

## 1. User Stories

### **Required (Must-have)**
- User can view a new inspirational quote on the Home screen.
- User can log today’s mood (happy / okay / sad).
- User can save the current quote to the Favorites list.

### **Optional (Nice-to-have)**
- User can view a mood history screen showing past mood entries.
- User receives a daily notification reminding them to open the app.
- User can share a quote through Messages or social media.
- User can pick from more mood types (excited, stressed, tired, etc.).

---

## 2. Screen Archetypes

### **Home Screen**
- Shows daily quote from API
- User can select mood
- User can save quote to Favorites

### **Favorites Screen**
- Shows list of saved quotes
- User can remove quotes from favorites

### **Mood History Screen** (optional)
- Shows past mood entries (date + mood)

---

## 3. Navigation

### **Tab Navigation (Tab to Screen)**
- **Home** → Daily quote + mood logging  
- **Favorites** → List of saved quotes  
- **History** (optional) → Mood history  

### **Flow Navigation (Screen to Screen)**

**Home Screen**  
→ Favorites (via tab)  
→ Mood History (via tab)  
→ Stays on Home after mood logging  
→ Stays on Home after saving quote  

**Favorites Screen**  
→ Home (tab)  
→ Mood History (tab)

**Mood History Screen**  
→ Home (tab)  
→ Favorites (tab)

---

# Wireframes

Simple layout:
- Home: quote text, mood buttons, save button
- Favorites: list of saved quotes
- History: list of moods by day

---

# Schema

## Models

### **Quote**
| Property | Type | Description |
|---------|------|-------------|
| id | String | unique identifier |
| text | String | quote text |
| author | String | quote author (optional) |
| isFavorite | Bool | stored locally |

### **MoodEntry**
| Property | Type | Description |
|----------|------|-------------|
| date | Date | specific day |
| mood | String | mood selected by user |

---

# Networking

## **Quote API (Example using zenquotes.io)**

### **Home Screen**
**[GET]** `https://zenquotes.io/api/today`  
- Retrieves the daily quote  
- Response includes quote text + author  

### **Favorites Screen**
Local storage (no network requests required)

### **Mood History Screen**
Local storage (no network requests required)

---

## Parse / API Snippets (if needed later)

```swift
// Example API request for daily quote
func fetchQuote() {
    guard let url = URL(string: "https://zenquotes.io/api/today") else { return }
    URLSession.shared.dataTask(with: url) { data, _, _ in
        if let data = data {
            let quote = try? JSONDecoder().decode([Quote].self, from: data)
        }
    }.resume()
}

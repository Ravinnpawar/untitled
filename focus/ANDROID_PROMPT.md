# Android Studio prompt – FOCUS app

Paste the **Master prompt** into Gemini in Android Studio (Agent mode) inside a new
**Empty Activity (Jetpack Compose)** project. AI agents work better in small steps, so if
the output is incomplete, continue with the **Step prompts** one at a time, building and
running after each step.

---

## Master prompt

```
Build a native Android app called "FOCUS – Reels Control & Study Reminder" for college
students. It supports a research project: "Impact of Reels and Short Video Addiction on
Academic Concentration Among College Students". The app helps students see their reels
screen time, study in focused sessions, get study reminders and answer a research survey.
UI text is English with short Marathi subtitles (e.g. "Today · आज").

TECH STACK
- Kotlin, Jetpack Compose, Material 3 (Material You dynamic color on Android 12+,
  fallback teal brand palette: primary #0D9488, secondary #7C3AED, warning #C27C00,
  error #D1434B). Light + dark theme.
- MVVM + Clean-ish layers: ui / viewmodel / data (repository) / Room database.
- Hilt for DI, Room for storage, DataStore (Preferences) for settings,
  WorkManager + AlarmManager for reminders, Navigation Compose, Kotlin Coroutines + Flow.
- minSdk 26, targetSdk 35. No internet permission; all data stays on device.
- Charts: draw with Compose Canvas (no heavy chart libraries).

NAVIGATION
Bottom navigation bar with 5 destinations + settings icon in the top app bar:
Today · आज | Timer · अभ्यास | Reels · रील्स | Survey · प्रश्नावली | Tips · उपाय
First-launch onboarding (3 swipeable pages with illustrations/emoji, name input,
study goal & reels limit pickers, then permission explanations).

DATA MODEL (Room)
- StudySession(id, date: LocalDate, startTime, minutes, subject, distractions)
- ReelsEntry(id, date, time, minutes, app: InstagramReels|YouTubeShorts|FacebookReels|Other,
  source: MANUAL|AUTO)
- SurveyResponse(id, timestamp, year, gender?, reelsTime, platform, whenWatch, whileStudy,
  concentration 1-5, longerThanPlanned 1-5, sleep, incomplete, studyHours, wantApp, suggestion?)
- Settings in DataStore: name, studyGoalMin (default 120), reelsLimitMin (default 30),
  focusMin (25), breakMin (5), reminderTimes (list, default 18:00 and 21:00), bedtime (23:00),
  autoTrackEnabled.

SCREENS
1. Today · आज (dashboard)
   - Greeting with name and date.
   - Hero card: circular "Focus score" 0–100 (study goal progress = 60 pts, staying under
     reels limit = 40 pts, decreasing to 0 as usage exceeds limit).
   - Two stat cards: Study today (progress bar vs goal) and Reels today (progress bar
     vs limit; amber at 80%, red over limit). Streak card (consecutive days goal met) 🔥.
   - Contextual banner: red when reels limit crossed, amber when near, green when goal met.
   - 7-day grouped bar chart: study minutes (teal) vs reels minutes (amber).
   - Big "Start studying" button and quick chips "+5 / +10 / +15 / +30 min reels".
   - Today's activity timeline.
2. Timer · अभ्यास (Pomodoro)
   - Large animated circular progress ring with mm:ss, mode label Focus/Break
     (teal for focus, violet for break), motivational quote line.
   - Subject field with suggestions from past subjects; length chips 15/25/45/60.
   - Start / Pause / Resume, "End & save" (saves minutes done), Reset.
   - Must keep running when the app is in the background or screen is off: use a
     Foreground Service with an ongoing notification showing the countdown and
     Pause/Stop actions. Play sound + vibration when a phase ends, then auto-start break.
   - Distraction tracking: while a focus block runs, count each time the user opens
     Instagram / YouTube / Facebook (detected via UsageStatsManager events) or leaves
     the app; show the count and a gentle notification "Reels can wait — back to study!".
   - Optional "Do Not Disturb during focus" toggle (request ACCESS_NOTIFICATION_POLICY).
   - Today's sessions list with swipe-to-delete + undo snackbar.
3. Reels · रील्स
   - AUTO TRACKING: with the user's permission (PACKAGE_USAGE_STATS, opened via
     Settings.ACTION_USAGE_ACCESS_SETTINGS with a clear explanation screen), read daily
     foreground time for com.instagram.android, com.google.android.youtube,
     com.facebook.katana using UsageStatsManager.queryEvents (compute from
     ACTIVITY_RESUMED/PAUSED pairs, not queryUsageStats, for accurate per-day values).
     Label it honestly: "Instagram / YouTube total time" because the OS cannot separate
     Reels/Shorts from the rest of the app.
   - MANUAL entry as fallback: app chips + minute chips + custom minutes + date picker.
   - Weekly per-app horizontal bar chart and daily average.
   - Limit alert: a WorkManager periodic job (15 min) checks today's usage and sends
     a notification at 80% and 100% of the reels limit (once per day each).
4. Survey · प्रश्नावली (research questionnaire)
   - Two tabs: "Fill survey" and "Results (n)".
   - Questions (English + Marathi subtitle), single-choice chips, required unless optional:
     1 Year of study: FY / SY / TY / PG-Other
     2 Gender (optional): Male / Female / Prefer not to say
     3 Daily reels time: <30 min / 30–60 min / 1–2 hrs / 2–3 hrs / >3 hrs
     4 Most used platform: Instagram Reels / YouTube Shorts / Facebook Reels / Other
     5 When watch most: Morning / Study breaks / During lectures / Late night
     6 Open reels while studying: Never / Sometimes / Often / Always
     7 "Reels make it hard to concentrate" 1–5 (1 strongly disagree, 5 strongly agree)
     8 "I plan a few minutes but watch much longer" 1–5
     9 Reels delay sleep: No / Sometimes / Yes, often
     10 Study remains incomplete due to reels: Never / Sometimes / Often / Always
     11 Daily study hours: <1 / 1–2 / 2–3 / >3
     12 Would a reminder/reels-control app help: Yes / Maybe / No
     13 Suggestion (optional free text, max 300 chars)
   - "Kiosk" flow: after submit show a thank-you screen ("धन्यवाद!") and reset for the
     next student. Highlight unanswered required questions and scroll to the first.
   - Results: KPI cards (responses, % watching 1hr+/day, % often/always while studying,
     % agreeing reels hurt concentration), a table "concentration difficulty vs daily reels
     time" (n, avg concentration, avg longer-than-planned, % study often incomplete),
     distribution bar charts for each question, recent suggestions.
   - Show a warning banner when fewer than 30 responses ("collect more before drawing
     conclusions") and a note that self-reported data shows correlation, not causation.
   - Export CSV (UTF-8 with BOM so Excel shows Marathi) and share via Android Sharesheet
     (FileProvider). Import CSV from other devices to merge responses (skip duplicates by id).
   - Never include fake/sample survey data.
5. Tips · उपाय
   - Expandable cards with emoji: phone in another room, 25-min blocks, turn off
     notifications, app limits in Digital Wellbeing (button opens it), no reels 1 hr before
     sleep, reels only as reward, move apps off home screen, study with a friend,
     plan tomorrow tonight, take real breaks.
6. Settings (from top bar)
   - Name, study goal, reels limit, focus/break length, dark mode (system/light/dark).
   - Study reminders: list of times with add (TimePicker) / delete; bedtime "phone away"
     reminder. Schedule with AlarmManager setExactAndAllowWhileIdle (fallback inexact if
     SCHEDULE_EXACT_ALARM not granted); reschedule on BOOT_COMPLETED.
     Reminder text adapts: "45 min left for today's goal — start a block".
   - Permission status rows (Notifications, Usage access, Exact alarms, DND) with
     "Grant" buttons.
   - Backup/restore all data as JSON via Storage Access Framework; "Reset tracker".

NOTIFICATIONS
Channels: Timer (low, ongoing), Reminders (high), Limit alerts (high). Request
POST_NOTIFICATIONS on Android 13+. Tapping a notification deep-links to the right screen.

HOME SCREEN WIDGET (Glance)
Small widget: today's study min vs goal, reels min vs limit, and a "Start focus" button.

UI / UX QUALITY
- Clean, modern, friendly look: rounded 20dp cards, generous spacing, large numbers
  for stats, smooth animations (animateFloatAsState for rings/bars, AnimatedContent
  for timer digits), haptic feedback on buttons.
- Edge-to-edge, proper insets, supports font scaling and TalkBack content descriptions.
- Use Noto Sans Devanagari-compatible default fonts so Marathi renders correctly.
- Empty states with friendly illustrations/emoji and a hint what to do.

QUALITY
- Unit tests for focus score, streak and survey cross-tab calculations; a Room DAO test.
- No crashes on rotation or process death (timer state persisted).
- Give me the full project structure first, then generate the files step by step.
```

---

## Step prompts (use if the agent stops halfway)

1. `Set up the project: Gradle dependencies (Compose BOM, Material3, Navigation, Hilt, Room, DataStore, WorkManager, Glance), theme with teal palette + dynamic color, and the bottom-navigation scaffold with 5 empty screens and a Settings route.`
2. `Create the Room entities, DAOs, database, DataStore settings repository and Hilt modules described earlier.`
3. `Build the Today dashboard screen and its ViewModel: focus score ring, study/reels stat cards, streak, limit banner, 7-day Canvas bar chart, quick-add reels chips and activity timeline.`
4. `Build the Pomodoro Timer screen with a Foreground Service that survives background/screen-off, ongoing notification with pause/stop actions, auto break, sound/vibration, End & save, and distraction counting.`
5. `Implement usage-access auto tracking with UsageStatsManager.queryEvents for Instagram, YouTube and Facebook, the permission explanation screen, manual entry fallback, weekly per-app chart and a WorkManager job for 80%/100% limit notifications.`
6. `Build the Survey screens: the 13-question form with validation and kiosk thank-you flow, the Results tab with KPI cards, concentration-vs-reels-time table and distribution charts, and CSV export/share/import.`
7. `Build Tips and Settings screens, AlarmManager study/bedtime reminders with BOOT_COMPLETED rescheduling, permission status rows and JSON backup/restore.`
8. `Add onboarding, the Glance home-screen widget, unit tests for score/streak/cross-tab, and polish animations, empty states and accessibility.`

---

## Notes for your report

- **Real screen time (auto tracking):** unlike the web prototype, the Android app can read
  real Instagram/YouTube/Facebook usage with *Usage Access* permission. Android only reports
  time per app, so it can't separate Reels/Shorts from the rest of the app.
- **Reminders and timer:** these keep working in the background (foreground service +
  alarms), which the browser version could not do.
- **Play Store:** apps that ask for Usage Access must explain why it's needed. Blocking other
  apps outright needs an Accessibility Service, which Google Play restricts, so this prompt
  uses notifications/nudges instead.

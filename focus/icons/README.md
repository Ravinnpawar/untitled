# FOCUS app icon

A study-timer ring (white arc, ~80% full) around an open book, on a teal gradient. The amber dot
is the timer's progress head, the same accent colour the app uses for reels.

| File | Use |
|---|---|
| `icon.svg` | Master icon (rounded square), any size |
| `ic_launcher_foreground.svg` / `_background.svg` / `_monochrome.svg` | Android adaptive-icon layers (glyph kept inside the 66 dp safe zone) |
| `play-store-512.png` | Google Play listing icon (512×512, full-bleed; Play applies the mask) |
| `android/res/` | Ready-made `mipmap-*` PNGs (mdpi–xxxhdpi) + `mipmap-anydpi-v26/ic_launcher*.xml` (adaptive + Android 13 themed icon) |
| `web/` | Favicon, Apple touch icon, 192/512 PWA icons |

**Android Studio:** copy the folders in `android/res/` into `app/src/main/res/` (replace the
existing `ic_launcher*` files), and keep `android:icon="@mipmap/ic_launcher"` and
`android:roundIcon="@mipmap/ic_launcher_round"` in `AndroidManifest.xml`.
Alternatively, use **File → New → Image Asset**: Foreground = `ic_launcher_foreground.svg`,
Background = `ic_launcher_background.svg` (or colour `#0F766E`).

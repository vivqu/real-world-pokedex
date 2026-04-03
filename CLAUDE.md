# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Real World Pokedex** — an iOS and Android app that lets users point their camera at an animal, classifies it using image recognition, and displays it as a Pokédex entry. Target platforms are iOS and Android (web is not a priority).

## Project Structure

The app lives inside the `real-world-pokedex/` subdirectory. All commands below should be run from there.

```
real-world-pokedex/
  app/              # Expo Router file-based routing
    _layout.tsx     # Root stack navigator (Stack + ThemeProvider)
    modal.tsx       # Modal screen
    (tabs)/         # Tab group
      _layout.tsx   # Tab navigator config
      index.tsx     # Home tab
      explore.tsx   # Explore tab
  components/       # Shared UI components
  constants/
    theme.ts        # Colors (light/dark) and Fonts (platform-specific)
  hooks/
    use-color-scheme.ts   # Color scheme detection (native)
    use-color-scheme.web.ts  # Color scheme detection (web)
    use-theme-color.ts    # Resolves themed color values
```

## Commands

```bash
cd real-world-pokedex

npm install          # Install dependencies
npm run start        # Start Expo dev server (opens QR for Expo Go)
npm run ios          # Start with iOS simulator
npm run android      # Start with Android emulator
npm run web          # Start web version
npm run lint         # Run ESLint
```

## Architecture

**Routing:** Uses Expo Router (file-based). The root `app/_layout.tsx` wraps the app in React Navigation's `ThemeProvider` and defines a Stack with a `(tabs)` group and a `modal` screen.

**Theming:** Light/dark mode is handled through:
- `constants/theme.ts` — `Colors` (light/dark palettes) and `Fonts` (platform-specific font stacks)
- `hooks/use-theme-color.ts` — resolves a color key from `Colors` given the current scheme, with optional per-component overrides
- `ThemedText` / `ThemedView` — wrapper components that consume `useThemeColor`

**Path aliases:** `@/` maps to the `real-world-pokedex/` root (configured in `tsconfig.json`).

**Platform-specific files:** The `.ios.tsx` / `.web.ts` suffix convention is used (e.g., `icon-symbol.ios.tsx`, `use-color-scheme.web.ts`) — Metro/Expo resolves these automatically.

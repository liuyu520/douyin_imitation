# Douyin-Vue Project Context

## Project Overview

`douyin-vue` is a high-fidelity mobile short video application imitating Douyin (TikTok). It serves as a "best practice" example for mobile Vue applications, aiming for native-app-like smoothness.

**Key Technologies:**
*   **Framework:** Vue 3 (Composition API)
*   **Build Tool:** Vite 5
*   **Language:** TypeScript
*   **State Management:** Pinia
*   **Routing:** Vue Router 4
*   **HTTP Client:** Axios
*   **Mocking:** `axios-mock-adapter` & `mockjs` (Data is stored locally in `public/data` or generated)
*   **Styling:** Less

## Building and Running

The project uses `npm` (and `pnpm` lockfile is present).

### Installation
```bash
npm install
# or
pnpm install
```

### Development Server
Starts the local development server at `http://localhost:3000`.
**Note:** You must switch your browser to **Mobile Mode** (Chrome: F12 -> Ctrl+Shift+M) to view the app correctly.
```bash
npm run dev
```

### Production Build
Builds the application for production to the `dist` directory.
```bash
npm run build
```

### Preview Production Build
Locally preview the production build.
```bash
npm run preview
```

### Linting & Formatting
```bash
# Run ESLint
npm run lint

# Format code with Prettier
npm run format
```

## Project Structure

*   `src/api/`: API definition files.
*   `src/assets/`: Static assets (images, less styles).
    *   `src/assets/less/index.less`: Global styles entry.
*   `src/components/`: Reusable Vue components.
*   `src/config/`: Configuration files (e.g., base URLs).
*   `src/mock/`: Mock data setup using `axios-mock-adapter`.
*   `src/pages/`: Application views/pages (Home, Message, Me, etc.).
*   `src/router/`: Vue Router configuration.
*   `src/store/`: Pinia stores.
*   `src/utils/`: Utility functions and hooks.
    *   `src/utils/bus.ts`: Event bus implementation.
*   `node/`: Node.js scripts for data processing.

## Development Conventions

*   **Mobile-First:** The app is designed strictly for mobile viewports. Always test in mobile emulation mode.
*   **Mock Data:** The backend is simulated via `axios-mock-adapter`. API calls are intercepted and served from local JSON data or generated on the fly. See `src/main.ts` for initialization (`startMock()`).
*   **Global Event Bus:** A lightweight event bus (`src/utils/bus.ts`) is used for cross-component communication where props/Pinia might be overkill.
*   **Custom Directives:** Includes custom directives like `v-click` (handled in `src/main.ts`).
*   **Interaction Handling:** `HTMLElement.prototype.addEventListener` is monkey-patched in `src/main.ts` to differentiate between clicks and swipes/moves, preventing accidental clicks during scrolling.
*   **Path Alias:** `@` maps to the `src/` directory.

## Key Configuration

*   **Vite (`vite.config.ts`):** Includes manual chunking strategy, CDN import configuration (for production), and alias setup.
*   **TypeScript (`tsconfig.json`):** Standard Vue + TS setup, referencing `tsconfig.app.json` and `tsconfig.node.json`.

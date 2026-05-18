# CSS-in-JS, SSR, and React 19 (v5)

Use this reference when the v5 task involves the styling engine, server-side rendering, legacy browser compatibility, or running antd v5 on React 19.

Source: `https://github.com/ant-design/ant-design/tree/5.29.3/docs/react` (`server-side-rendering`, `compatible-style`, `v5-for-19`, `customize-theme`).

## Styling engine

- v5 ships CSS-in-JS via `@ant-design/cssinjs`. Less is not used; `babel-plugin-import` is unsupported; `antd/dist/antd.css` is removed.
- For a base CSS reset only, import `antd/dist/reset.css` once at the entry.
- Drive themes via `ConfigProvider` `theme` (global / component / algorithm). Do not override compiled cssinjs class names; use `classNames`/`styles` props or component tokens.

## Server-side rendering (Next.js, Remix, etc.)

Core imports:

```tsx
import { StyleProvider, createCache, extractStyle } from '@ant-design/cssinjs';
```

Render flow:
1. Create a cache per request: `const cache = createCache();`
2. Wrap the React tree: `<StyleProvider cache={cache}>{app}</StyleProvider>`.
3. After render, call `extractStyle(cache)` to get a string of `<style>` tags.
4. Inject that string into the HTML `<head>` so the browser has styles before hydration.

### Next.js Pages Router
- Implement in `pages/_document.tsx` via `getInitialProps`. Wrap the rendered app in `StyleProvider`, call `extractStyle(cache)` after render, then add the resulting markup to the document `<head>`.

### Next.js App Router
- Use a Client Component style registry that builds the cache lazily and flushes via `useServerInsertedHTML` in a layout. Each request must get its own cache instance.

### Pre-baked CSS (optional)
- For multi-page apps that want browser-cacheable CSS, use `@ant-design/static-style-extract` to generate a CSS file at build time. Add a `predev`/`prebuild` script that runs the extractor (typically via `ts-node`).
- Trade-off: smaller initial HTML, extra build step, separate output per theme.

## Legacy browser compatibility

Targets that lack `:where()` (Chrome <88) or CSS logical properties (Chrome <89):

```tsx
import { StyleProvider, legacyLogicalPropertiesTransformer } from '@ant-design/cssinjs';

<StyleProvider hashPriority="high" transformers={[legacyLogicalPropertiesTransformer]}>
  <App />
</StyleProvider>
```

- `hashPriority="high"` removes the `:where()` wrapper so generated selectors use plain class selectors (and therefore higher specificity).
- `legacyLogicalPropertiesTransformer` rewrites `margin-inline-start` etc. back to physical properties.
- Trade-off: raising specificity may collide with existing global CSS — audit any `.ant-*` overrides afterwards.

## React 19 compatibility

v5 supports React 16–18 natively. On React 19, the changed `react-dom` exports break:
- Wave / ripple feedback on focusable components.
- Static methods on `Modal`, `notification`, `message`, `Drawer` (the hook forms keep working).

Two options, in order of preference:

### Option A — official patch (default)
```bash
npm install @ant-design/v5-patch-for-react-19
```
Import once at the application entry:
```tsx
import '@ant-design/v5-patch-for-react-19';
```
The patch ships in the v5 line only; v6 removes it.

### Option B — `unstableSetRender` (UMD / micro-frontends)
Only use this when the patch can't be loaded at the entry (e.g. UMD bundles, sub-applications mounted by a host shell).

```tsx
import { unstableSetRender } from 'antd';
import { createRoot } from 'react-dom/client';

unstableSetRender((node, container) => {
  container._reactRoot ||= createRoot(container);
  const root = container._reactRoot;
  root.render(node);
  return async () => {
    await new Promise((resolve) => setTimeout(resolve, 0));
    root.unmount();
  };
});
```

### Regardless of patch
Migrate static method call sites to their hook forms:
- `App.useApp()` → context-aware `message` / `notification` / `modal`.
- `message.useMessage()`, `notification.useNotification()`, `Modal.useModal()` for finer scope.

Hook forms are required for correct theme/locale inheritance in v5 and are the only forms that survive in v6.

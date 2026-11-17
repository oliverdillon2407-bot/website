# Agent Instructions

## Project overview

- This repository is a small, static e-commerce storefront named **Omnibus**.
- The complete application is implemented in [index.html](index.html): HTML, CSS, and client-side JavaScript live together in that one file.
- [README.md](README.md) is the only project documentation and defines the local run command.
- There is no package manager, build system, transpiler, test framework, backend, or database.

## Working conventions

- Prefer surgical edits to [index.html](index.html). Only split code into separate files when the task explicitly requires a more maintainable structure.
- Preserve the existing plain HTML/CSS/JavaScript style and camelCase function names.
- Use the existing CSS variables, card layout, buttons, modal, and filter bar patterns for consistent UI changes.
- Keep the store usable in a browser with JavaScript enabled and no external build step.
- Do not introduce dependencies unless the task explicitly requires them.
- Update [README.md](README.md) when changing setup, run, or user-facing usage instructions.

## Data and behavior

- Product data is stored in `localStorage` under `omnibus_products`.
- `defaultProducts` supplies the initial catalog; `saveProducts()` persists catalog changes.
- Treat `p.name`, `p.desc`, `p.category`, `p.image`, and `p.link` as part of the stored product shape.
- Preserve both purchase paths:
  - a valid payment `p.link` opens a `Buy Now` external link;
  - otherwise `openOrderModal()` collects an order and opens the configured mailto flow.
- The owner area is toggled entirely in the browser by `isAdmin`; a successful PIN reveal is not server-side authorization.
- Uploaded images are converted with `FileReader` to data URLs and stored in `localStorage`. Be mindful of browser storage limits and preserve the existing image upload flow unless changing it intentionally.
- Maintain category filtering and the search behavior in `renderProducts()`.

## Editing guidance

- Escape or encode data that is inserted into HTML attributes or `innerHTML`; do not introduce unsafe user-controlled string interpolation.
- Validate new form fields in the browser and provide clear existing-style alert messages for invalid input.
- Preserve keyboard and basic accessibility behavior: use semantic controls and labels where practical, keep the modal understandable, and do not remove focus-visible or hover states without a replacement.
- Keep responsive behavior through the existing CSS grid and flex patterns.
- When changing IDs or function names, update every call site in the HTML and script together.
- Do not claim the PIN, mail address, or payment URLs are production-ready when placeholder values remain.

## Validation

- Run a local static server from the repository root:

  ```sh
  python3 -m http.server 8000
  ```

- Open `http://localhost:8000` and verify the relevant UI in a browser.
- For focused checks, use:

  ```sh
  curl -I http://localhost:8000/
  ```

- There is no automated test suite or lint command. For changes, manually test the affected flow, including relevant console output and the final browser state.
- If browser automation is available, prefer a focused smoke test over adding a new test framework.

# Telegram Fiscal Receipt WebApp (54-FZ QR-Code Builder)

A lightweight, serverless Single Page Application (SPA) built as a **Telegram Mini App (TMA)**. It provides a clean, native-feeling user interface to manually enter, pre-fill, and validate Russian fiscal receipt parameters in strict accordance with Federal Law **54-FZ**. 

Once validated, the app compiles the data into a standard query string format required for fiscal QR-code generation and passes it directly back to the Telegram Bot via the official Telegram WebApp SDK.

---

## 🚀 Features

- **Zero Backend (Serverless):** Runs entirely on the client side. Built using pure vanilla HTML5, CSS3, and JavaScript (ES6+). Perfect for free hosting via **GitHub Pages**.
- **Telegram Mini App SDK Integration:** Seamlessly interacts with `window.Telegram.WebApp`. Utilizes the native `MainButton` for form submission and automatically closes the webview upon completion.
- **Dynamic Pre-fill & Edit Mode:** Parses incoming URL search parameters (e.g., `?t=...&s=...&fn=...`) on load to pre-populate the form, automatically translating technical strings back into human-readable input values.
- **Strict Real-Time Validation:** 
  - **Date/Time (`t`):** Uses an elegant datetime picker, strictly blocking future dates.
  - **Amount (`s`):** Enforces a decimal format with exactly two decimal places, automatically replacing commas with dots.
  - **Fiscal Parameters (`fn`, `i`, `fp`):** Strips non-numeric characters on the fly, forcing strict digit length boundaries (e.g., exactly 16 digits for the Fiscal Drive).
  - **Operation Type (`n`):** Maps human-readable calculation vectors (Inflow/Outflow/Returns) to proper numeric flags.
- **Bi-directional Mobile Keypads:** Employs precise `inputmode` attributes (`decimal`, `numeric`) to trigger the correct native virtual keyboards on iOS and Android.
- **Smart Localization (RU / EN):** Automatically detects the user's language from their Telegram profile and instantly translates all UI labels, placeholders, and validation error messages.
- **Native Look & Feel:** Features a single-page card layout mimicking native Telegram/iOS/Android settings. Fully reactive to instant light/dark theme toggles using official Telegram CSS variables.

---

## 🛠️ Technical 54-FZ String Output

Upon successful validation and clicking the native Telegram **Submit** button, the WebApp compiles the inputs into the standard query string used for Russian fiscal QR codes:

```text
t=YYYYMMDDTHHMM&s=0.00&fn=0000000000000000&i=0&fp=0&n=1
```

The resulting string is safely transmitted back to your Telegram bot backend using `tg.sendData()`.

---

## 📂 Repository Structure

- `index.html` — The entire codebase. Contains structured HTML markup, a reactive CSS stylesheet driven by Telegram theme variables, and modular vanilla JS logic for validation, pre-filling, and SDK interaction.

---

## 🔧 Local Setup & Deployment

1. Clone this repository to your local machine or fork it on GitHub.
2. Enable **GitHub Pages** in your repository settings to host the `index.html` file publicly.
3. Link the deployment URL to your Telegram Bot using `@BotFather` (set up a Menu Button or a inline button leading to your WebApp URL).

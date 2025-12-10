# Lab - 2:

**Plan — What you'll do**
- Create a small project with `index.html`, optional `styles.css` and `app.js`.
- Use GitHub Copilot in VS Code to autogenerate form structure and validation snippets.
- Implement two responsive variants: Bootstrap (CDN) and Tailwind (Play CDN).
- Add client-side validation (HTML5 + JS) and accessibility attributes.
- Run and test the pages locally, commit to GitHub.

**README.md** (copy this file to your repo root)

- **Title:** Build a responsive login form with validation using Copilot
- **Overview:** Step-by-step lab to build a responsive, accessible login form using GitHub Copilot. Includes two responsive approaches: Bootstrap and Tailwind (CDN), and client-side validation using HTML5 + JavaScript.

**Prerequisites**
- **Code editor:** `Visual Studio Code` with `GitHub Copilot` extension installed and signed-in.
- **Git:** configured (`git config --global user.name`, `user.email`).
- **Local server (optional):** Live Server VS Code extension or Python.
- **Browser:** modern browser (Chrome/Edge/Firefox).

**Project files**
- `index-bootstrap.html` — Bootstrap variant (CDN).
- `index-tailwind.html` — Tailwind variant (Play CDN).
- `styles.css` — optional custom styles.
- `app.js` — form validation scripts.
- `README.md` — this file.

**Quick setup**
- Create project folder and files:
  - `index-bootstrap.html`
  - `index-tailwind.html`
  - `styles.css`
  - `app.js`
- Open folder in VS Code and enable Copilot suggestions.

**How to open/run locally**
- Using Live Server extension: right-click `index-bootstrap.html` or `index-tailwind.html` → `Open with Live Server`.
- Or with Python (PowerShell):
```powershell
python -m http.server 5500
# Open http://localhost:5500/index-bootstrap.html
```

**Copilot usage tips (prompts to use in file comments or at top of a new file)**
- Prompt to generate structure:
  - `// Generate a responsive login form with email, password, remember me checkbox, and submit button. Add ARIA labels and client-side validation messages.`
- Prompt to add Bootstrap classes:
  - `// Use Bootstrap 5 classes to center a card with a login form and make it responsive.`
- Prompt to add Tailwind classes:
  - `// Use Tailwind CSS utility classes to create a centered login form with responsive layout and accessible labels.`
- Prompt for JS validation:
  - `// Add JavaScript that validates email format, requires password >= 8 chars, shows inline error messages, and prevents submit if invalid.`

**Step-by-step — Bootstrap variant**
1. Create `index-bootstrap.html` and add this content (Bootstrap via CDN, minimal JS hooks):
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Login — Bootstrap</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body class="bg-light">
  <main class="d-flex align-items-center justify-content-center vh-100">
    <div class="card shadow-sm w-100" style="max-width:420px;">
      <div class="card-body">
        <h5 class="card-title text-center mb-4">Sign in</h5>
        <form id="loginForm" novalidate>
          <div class="mb-3">
            <label for="email" class="form-label">Email address</label>
            <input type="email" class="form-control" id="email" name="email" required aria-describedby="emailHelp">
            <div class="invalid-feedback">Please enter a valid email.</div>
          </div>
          <div class="mb-3">
            <label for="password" class="form-label">Password</label>
            <input type="password" class="form-control" id="password" name="password" required minlength="8" aria-describedby="pwdHelp">
            <div class="invalid-feedback">Password must be at least 8 characters.</div>
          </div>
          <div class="mb-3 form-check">
            <input type="checkbox" class="form-check-input" id="remember" name="remember">
            <label class="form-check-label" for="remember">Remember me</label>
          </div>
          <button type="submit" class="btn btn-primary w-100">Sign in</button>
        </form>
      </div>
    </div>
  </main>

  <script src="app.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```
2. Let Copilot help: open `index-bootstrap.html`, add the prompt comment at top, accept/refine suggestions for classes and structure.

**Step-by-step — Tailwind variant (Play CDN for demo)**
1. Create `index-tailwind.html`:
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <title>Login — Tailwind</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="styles.css">
</head>
<body class="bg-gray-50">
  <main class="min-h-screen flex items-center justify-center">
    <div class="w-full max-w-md bg-white rounded-lg shadow p-6">
      <h2 class="text-2xl font-semibold text-center mb-4">Sign in</h2>
      <form id="loginFormTailwind" novalidate>
        <label for="email" class="block text-sm font-medium mb-1">Email address</label>
        <input id="email" name="email" type="email" required class="w-full px-3 py-2 border rounded mb-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" aria-describedby="emailHelp">
        <p class="text-sm text-red-600 hidden" id="emailError">Enter a valid email.</p>

        <label for="password" class="block text-sm font-medium mt-3 mb-1">Password</label>
        <input id="password" name="password" type="password" required minlength="8" class="w-full px-3 py-2 border rounded mb-2 focus:outline-none focus:ring-2 focus:ring-indigo-500" aria-describedby="pwdHelp">
        <p class="text-sm text-red-600 hidden" id="pwdError">Password must be at least 8 characters.</p>

        <div class="flex items-center mt-4 mb-4">
          <input id="remember" name="remember" type="checkbox" class="mr-2">
          <label for="remember" class="text-sm">Remember me</label>
        </div>

        <button type="submit" class="w-full bg-indigo-600 text-white py-2 rounded hover:bg-indigo-700">Sign in</button>
      </form>
    </div>
  </main>

  <script src="app.js"></script>
</body>
</html>
```
2. Use Copilot to iterate on Tailwind utility classes and accessibility attributes.

**Client-side validation script (`app.js`)**
- Use same file for both pages; script detects form id(s). Add this content:
```javascript
// app.js
document.addEventListener('DOMContentLoaded', () => {
  const forms = [
    document.getElementById('loginForm'),
    document.getElementById('loginFormTailwind')
  ].filter(Boolean);

  forms.forEach(form => {
    form.addEventListener('submit', function (e) {
      e.preventDefault();
      let valid = true;

      // email validation
      const email = form.querySelector('input[type="email"]');
      if (email) {
        const ok = /^\S+@\S+\.\S+$/.test(email.value.trim());
        toggleFieldState(email, ok, 'Please enter a valid email.');
        valid = valid && ok;
      }

      // password validation
      const password = form.querySelector('input[type="password"]');
      if (password) {
        const ok = password.value.trim().length >= 8;
        toggleFieldState(password, ok, 'Password must be at least 8 characters.');
        valid = valid && ok;
      }

      if (valid) {
        // Simulate successful submit — replace with real submit or AJAX
        alert('Form valid — proceed to submit (demo).');
        form.reset();
        clearAllStates(form);
      }
    });
  });

  function toggleFieldState(input, ok, message) {
    const parent = input.closest('div') || input.parentElement;
    // Bootstrap handling
    if (input.classList.contains('form-control')) {
      input.classList.toggle('is-invalid', !ok);
      // invalid-feedback element exists in markup for bootstrap
    } else {
      // Tailwind handling: show/hide error <p> sibling if present
      const id = input.id;
      const err = document.getElementById(id + 'Error');
      if (err) {
        err.textContent = ok ? '' : message;
        err.classList.toggle('hidden', ok);
      }
      input.classList.toggle('border-red-600', !ok);
    }
  }

  function clearAllStates(form) {
    const invalids = form.querySelectorAll('.is-invalid, .border-red-600');
    invalids.forEach(el => el.classList.remove('is-invalid', 'border-red-600'));
    const errors = form.querySelectorAll('[id$="Error"]');
    errors.forEach(e => { e.classList.add('hidden'); e.textContent = ''; });
  }
});
```

**Optional `styles.css` (small visual tweaks)**
```css
/* styles.css */
body { font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial; }
.card { border-radius: 0.75rem; }
```

**Testing the forms**
- Launch the chosen HTML file with Live Server or `http://localhost:5500/index-bootstrap.html`.
- Try submitting empty or invalid values — inline errors should appear.
- Try a valid email and password (>=8 chars) — alert demonstrates success (replace with real submit/AJAX in production).

**Accessibility & best practices**
- **Labels:** Use `<label for="...">` tied to inputs.
- **ARIA:** Add `aria-describedby` when showing error text.
- **Keyboard:** Ensure focus outlines preserved; do not remove outlines without replacement.
- **Feedback:** Prefer inline error messages and summarised error for screen readers.
- **Production:** Use server-side validation in addition to client-side checks, and build Tailwind properly (not via CDN) for production.

**Copilot prompt examples (copy/paste)**
- "Create a responsive login form using Bootstrap 5 centered on the page with email, password, remember checkbox, and accessible labels."
- "Generate Tailwind markup for a login card centered vertically and horizontally, with email and password fields and a submit button."
- "Add a JavaScript function that validates email format and password length and shows inline error messages."

**Commit & push to GitHub**
- Example PowerShell commands:
```powershell
git init
git add .
git commit -m "feat: add responsive login form examples (Bootstrap & Tailwind) with validation"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo>.git
git push -u origin main
```

**Troubleshooting**
- Copilot not suggesting: confirm extension is enabled and you're signed in to GitHub.
- Tailwind CDN differences: Play CDN is for prototyping, not production. For production use PostCSS + Tailwind CLI.
- Validation not showing: ensure `novalidate` is present on form if you use custom JS handling.

**Next steps / extensions**
- Replace demo alert with an AJAX POST to an API endpoint.
- Add server-side validation sample in Node/Express or Spring Boot.
- Add unit tests (Jest for JS) or E2E tests (Playwright) for the form.

**License**
- This lab content is MIT-like for learning/demo purposes. When using Copilot-generated code in public projects, follow GitHub Copilot usage and licensing guidance.

If you want, I can:
- scaffold these files into your workspace now; or
- generate a ready-to-push repo zip with both variants and GitHub Actions to preview pages. Which would you prefer?

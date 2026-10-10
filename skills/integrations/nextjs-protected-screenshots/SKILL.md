---
name: nextjs-protected-screenshots
description: Automated Playwright screenshot capture of authentication-protected Next.js applications with session cookie injection, viewport scaling, and redirect bypass.
version: 1.0.0
metadata:
  category: integrations
  tags: [nextjs, playwright, screenshot, testing, automation, visual-qa]
---

# Protected Next.js App Screenshot Capture 📸🔒

## 🛠️ Playwright Session Injection Pattern

Next.js apps using middleware (`middleware.ts`) automatically redirect unauthorized visitors to `/login`. To allow headless agents to inspect authenticated dashboards:

```python
import os
from playwright.sync_api import sync_playwright

def capture_protected_dashboard(target_url, auth_cookie_value, output_path="dashboard.png"):
    with sync_playwright() as p:
        browser = p.chromium.launch(headless=True)
        context = browser.new_context(
            viewport={"width": 1440, "height": 900},
            device_scale_factor=2
        )
        
        # Inject session cookie prior to navigation
        context.add_cookies([
            {
                "name": "next-auth.session-token",  # Or your app's session cookie name
                "value": auth_cookie_value,
                "domain": "localhost",
                "path": "/"
            }
        ])
        
        page = context.new_page()
        page.goto(target_url, wait_until="networkidle")
        page.screenshot(path=output_path, full_page=True)
        browser.close()
        print(f"Captured: {output_path}")

if __name__ == "__main__":
    cookie = os.environ.get("TEST_SESSION_TOKEN", "mock-session-token")
    capture_protected_dashboard("http://localhost:3000/dashboard", cookie)
```

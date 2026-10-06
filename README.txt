THT CUSTOMER SURVEY + ADMIN DASHBOARD

1. Apps Script
   - Replace current Code.gs with the new Code.gs in this package.
   - Deploy > Manage deployments > Edit > New version > Deploy.
   - Keep the same Web App URL.

2. GitHub Pages
   - Replace ONLY index.html in the existing repo.
   - Keep the existing assets folder:
       assets/logo.jpg
       assets/hero.jpg
   - Existing app.js and style.css can remain; this index.html no longer uses them.

3. Access
   - Customer: no password.
   - Admin: PIN is checked by Apps Script backend.
   - Admin PIN configured in Code.gs: 8888
   - Login state is kept only for the current browser tab/session.

4. Dashboard
   - Overview
   - Analysis
   - Customers
   - Issues & Actions (read-only)

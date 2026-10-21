# Muhammed Yazeen KA — Data Analyst Portfolio

An editorial, narrative-driven portfolio for a Data Analyst (SQL · Python · Power BI · Excel). Every project is told as a short data story: **Context → Friction → Analytical Approach → Business Impact**.

**Live site:** https://your-site.vercel.app *(replace with your deployed URL)*

## Highlights

- Single-file site: HTML, Tailwind CSS (CDN) and vanilla JavaScript. No build step.
- Editorial design with a warm-to-dark palette, serif display type and a grain overlay, inspired by [obsidianassembly.com](https://obsidianassembly.com). No assets were copied.
- Scroll-reveal animations, hero parallax, a scroll-progress line and a cursor-trail animation (disabled on touch devices and for `prefers-reduced-motion`).
- Interactive project filter: All / Python / SQL / Excel / Power BI.
- Contact form that stores every enquiry in a Google Sheet and emails a copy to the owner.

## Projects featured

| # | Project | Stack |
|---|---------|-------|
| I | Global Employment Market Analyzer | Python, Pandas, NumPy, Streamlit, REST APIs |
| II | Amazon-Style E-Commerce Revenue Dashboard | Python, SQLite, SQL, Excel, Power BI |
| III | HR and Workforce Analytics | SQL (CTEs, window functions), Excel, Pandas |
| IV | Crisis Economy Tracker | Python, NumPy, time-series analysis |

## Run locally

```bash
git clone https://github.com/yazeenworks/<repo-name>.git
cd <repo-name>
# open index.html in a browser, or serve it:
npx serve .
```

## Deploy (Vercel)

1. Push this repo to GitHub.
2. In Vercel choose **Add New → Project**, import the repo and click **Deploy**. No settings are needed for a static site.

## Contact form → Google Sheet

1. Create a Google Sheet, then open **Extensions → Apps Script** and paste:

```javascript
function doPost(e) {
  try {
    var p = e.parameter;
    if (p.website) return ContentService.createTextOutput('ok'); // spam trap
    var ss = SpreadsheetApp.getActiveSpreadsheet();
    var sh = ss.getSheetByName('Leads') || ss.insertSheet('Leads');
    if (sh.getLastRow() === 0) sh.appendRow(['Date', 'Name', 'Email', 'Message']);
    sh.appendRow([new Date(), p.name, p.email, p.message]);
    MailApp.sendEmail('YOUR_EMAIL', 'Portfolio enquiry from ' + p.name,
      'From: ' + p.name + ' <' + p.email + '>\n\n' + p.message, { replyTo: p.email });
    return ContentService.createTextOutput('ok');
  } catch (err) {
    return ContentService.createTextOutput('error');
  }
}
```

2. **Deploy → New deployment → Web app**, with *Execute as: Me* and *Who has access: Anyone*.
3. Paste the `/exec` URL into `const SHEET_URL=''` near the bottom of `index.html`.

Until `SHEET_URL` is set, the form falls back to a `mailto:` link.

## Structure

```
index.html   # markup, styles and scripts for the whole site
README.md
```

## Contact

- Email: muhdyaseen9562@gmail.com
- LinkedIn: [muhammed-yazeen-ka](https://linkedin.com/in/muhammed-yazeen-ka-52345332a)
- GitHub: [yazeenworks](https://github.com/yazeenworks)

© 2026 Muhammed Yazeen KA. All rights reserved.

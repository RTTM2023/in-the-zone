[README.md](https://github.com/user-attachments/files/32749528/README.md)
# In the Zone: set-up guide

In the Zone is a two-minute anonymous team check. Leaders create a check for their team, predict where the team sits, send a survey link, and see results once 4 people have responded.

There are two files:

- **index.html** is the web page. It goes on GitHub Pages.
- **Code.gs** is the script that stores answers in your Google Sheet. It stays in Google. **Never upload Code.gs to GitHub**, because it contains your admin password.

Set-up takes about an hour. You can try the page first in demo mode: open index.html in a browser and use the links in the dark bar at the top. Nothing is saved in demo mode.

---

## Part A: The Google Sheet (about 15 minutes)

1. Go to [sheets.google.com](https://sheets.google.com), signed in to your RTTM Google account.
2. Create a blank spreadsheet and name it **In the Zone: WFS**.
3. In the menu, choose **Extensions > Apps Script**. A new tab opens with some sample code.
4. Delete the sample code. Open **Code.gs**, copy everything, and paste it in.
5. Near the top, find this line and replace `change-me` with a strong password of your own:
   ```
   const ADMIN_PASSWORD = 'change-me';
   ```
   The programme view stays locked until you change it.
6. Click the **Save** icon.
7. In the dropdown next to **Run** at the top, choose **setup**, then click **Run**.
8. Google asks for permission. Click **Review permissions**, choose your account, then **Advanced**, then **Go to (your project name)**, then **Allow**. This warning is normal for a script you've written yourself.
9. Go back to your spreadsheet. You should now see two tabs: **Teams** and **Responses**.
10. Back in Apps Script, click **Deploy > New deployment**.
11. Click the gear icon next to "Select type" and choose **Web app**. Set:
    - Description: **In the Zone**
    - Execute as: **Me**
    - Who has access: **Anyone**
12. Click **Deploy**, then copy the **Web app URL**. It ends in `/exec`.

## Part B: Connect the page (2 minutes)

13. Open **index.html** in a text editor.
14. Near the top of the script, find the CONFIG block and paste your URL between the quotes:
    ```
    API_URL: "https://script.google.com/macros/s/.../exec",
    ```
15. Save the file. The demo bar disappears once the URL is in.

If you'd rather not edit code, send the URL back to Claude and it will do this step for you.

## Part C: Put it online with GitHub Pages (15 minutes)

16. On GitHub, create a new **public** repository called **in-the-zone**.
17. Choose **Add file > Upload files**, upload **index.html** only, and commit.
18. Go to **Settings > Pages**. Under Source, choose **Deploy from a branch**, branch **main**, folder **/ (root)**, and save.
19. After a minute or two, the page is live at:
    `https://YOUR-GITHUB-USERNAME.github.io/in-the-zone/`

**Optional:** paste that address into `SITE_URL` in the CONFIG block and upload index.html again. This keeps every generated link pointing at the right address.

## Part D: Test before it goes to WFS (30 minutes)

20. Open the page and create a test team.
21. Save the results link, then open the survey link on 4 different phones, or on one device using "Respond as a different person".
22. Open the results link. Check that it unlocks at 4 responses and that the graphs look right.
23. Open the programme view by adding `?admin=1` to the address, and log in with your password.
24. Ask Masichaba to open the page on a WFS work laptop, to check the company network doesn't block it.
25. Delete the test rows in both tabs of the Google Sheet. Keep the header row.

---

## The links you'll use

| What | Address | Who gets it |
|---|---|---|
| Start page | `https://YOUR-USERNAME.github.io/in-the-zone/` | Every leader, in the session |
| Programme view | the same address with `?admin=1` on the end | You only |

Each leader then gets two links of their own when they create their check: a survey link for their team, and a private results link.

## Good to know

**If a leader loses their results link:** open the programme view, find their team, and click **Copy results link**.

**If you change Code.gs later:** in Apps Script, go to **Deploy > Manage deployments**, click the pencil icon, set Version to **New version**, and click **Deploy**. The web address stays the same. If you skip this, your changes won't take effect.

**To change the response threshold:** edit `MIN_RESPONSES` in Code.gs and redeploy as above.

**Privacy:** the sheet stores only the team name, level, the leader's prediction, the 8 answers and a time for each response. No names, emails or device details. Only you can see the sheet unless you share it. Share results with WFS through the programme view or its CSV download, not by sharing the sheet.

**If a leader sees "Your team check wasn't created":** check that API_URL is pasted correctly, that the deployment's access is set to **Anyone**, and that you deployed a new version after any change.

**For another client:** make a copy of the Google Sheet (the script copies with it), deploy it, and put a copy of index.html in a new repository with the new URL and partner name in CONFIG.

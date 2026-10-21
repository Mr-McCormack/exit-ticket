# Exit Ticket

A free, live exit ticket and checkpoint tool for algebra classes.

- **Pick a question** from a built-in bank of 100+ algebra questions, sorted by topic and difficulty. You can also write your own.
- **Push it** to your class. It appears on students' laptops right away, with no logins, names, or phones.
- **Watch a live tally.** Equivalent math answers are grouped, so √8 and 2√2 count together.

Created by John McCormack, M.Ed. It's free to copy and use in your own classroom.

> **Before you start:** This is a do-it-yourself copy. You'll set up your own free accounts, so your classes and data stay completely separate from everyone else's. Setup takes about 30 minutes, one time. You don't need any coding experience.

---

## What you'll need

- A free **GitHub** account, which hosts the web page
- A free **Google** account, used only to create your Firebase database. A personal Gmail works best, because some school Google accounts block Firebase. You won't sign in with it day to day; you'll use a teacher PIN instead.

You won't need a credit card. Everything here runs on free plans.

---

## Step 1: Copy this project to your GitHub

1. Make a free GitHub account at **https://github.com/signup**.
   - Your username becomes part of your link (`yourname.github.io/exit-ticket/`), so choose one you're comfortable having students see.
2. While signed in, come back to this page and click **Fork** near the top right, then **Create fork**.

## Step 2: Turn on your web page

1. In **your** copy, click **Settings**, then **Pages** in the left menu.
2. Under **Source**, choose **Deploy from a branch**. Pick **main** and **/(root)**, then click **Save**.
3. Wait a minute or two, then refresh. You'll see **"Your site is live at…"** with your link. Save that link.

## Step 3: Create your free Firebase project

1. Go to **https://console.firebase.google.com** and sign in with your Google account.
2. Click **Create a project** (it may say **Add project**). Name it something like *Exit Ticket*. You can turn off Google Analytics.
3. The main menu is hidden behind the **☰** icon in the top-left corner. Google renames menu sections from time to time, so if a name below doesn't match exactly, look for the closest one.

## Step 4: Create the database

1. Open **☰** and find **Firestore Database** (it may be under *Build* or *Databases & Storage*). Click **Create database**.
2. If it asks for an edition, choose **Standard edition**.
3. Leave the database ID as `(default)` and keep the suggested location.
4. When it asks about security rules, choose **Start in production mode**. You'll add the real rules in Step 7.

## Step 5: Connect your page to your database

1. In Firebase, click the **gear icon** next to *Project Overview*, then **Project settings**.
2. Scroll to **Your apps** and click the web icon **`</>`**. Give it a nickname and click **Register app**. Leave **"Also set up Firebase Hosting"** unchecked.
3. Firebase shows a block of code. Copy only the lines **inside** `const firebaseConfig = { … };`, starting with `apiKey`. Ignore anything about `npm install`.
4. Back in **your** GitHub copy, click **`firebase-config.js`**, then the **pencil icon** ✏️.
5. **Delete the lines between the braces and paste in yours.** The file has the original author's settings in it, and your copy won't be yours until you replace them. It should look like this, with your own values:

   ```js
   export const firebaseConfig = {
     apiKey: "AIza...",
     authDomain: "exit-ticket-xxxxx.firebaseapp.com",
     projectId: "exit-ticket-xxxxx",
     storageBucket: "exit-ticket-xxxxx.firebasestorage.app",
     messagingSenderId: "1234567890",
     appId: "1:1234567890:web:abc123"
   };
   ```

6. Click **Commit changes**.

## Step 6: Allow the page to connect

1. In Firebase, open **☰ → Authentication** and click **Get started**.
2. On the **Sign-in method** tab, choose **Anonymous**, switch it to **Enable**, and click **Save**.
   - This lets the page connect without anyone creating an account. Your teacher PIN is what keeps students out of the teacher view.
3. Go to the **Settings** tab, then **Authorized domains**, then **Add domain**. Enter your GitHub Pages address without `https://`, like **`yourname.github.io`**.

## Step 7: Add the security rules

1. In **your** GitHub copy, click **`firestore.rules`** and copy all of it.
2. In Firebase, open **Firestore Database** and click the **Rules** tab.
3. Delete everything there, paste in the rules, and click **Publish**. You don't need to change anything in them.

## Step 8: Set your PIN and try it out

1. Open your **teacher view** by adding `?view=teacher` to the end of your link:
   `https://yourname.github.io/exit-ticket/?view=teacher`
2. Enter the starting PIN, **1234**. The page asks you to choose your own PIN right away. Use 6 or more characters, and don't type it while your screen is projected.
3. Open your **student link** (the same link *without* `?view=teacher`) in a second window. An Incognito/private window works well.
4. Back on the teacher view, pick a topic and click **Push ▶** on any question. It appears in the student window. Submit an answer and watch the tally.

That's it. Give students the link **without** `?view=teacher`. Posting it in your LMS or as a bookmark works well. Each computer you use as the teacher asks for your PIN once, then remembers it.

---

## Using it in class

| You want to… | Do this |
|---|---|
| Ask a question fast | Pick a topic and difficulty, then click **🎲 Push random**. It avoids questions you pushed recently. |
| Ask a specific question | Click **Push ▶** on it. |
| Change a stock question | Click **Edit**. Your version is saved, and **Reset to original** undoes it. |
| Write your own | Click **+ New**. Type the directions in plain words and the math in the math box. Type a new topic name to start your own topic. |
| Keep students from copying the majority | Click **Hide answers** before projecting. Only the response count shows. |
| Reveal the answer | Click **Show answers**, then **Show correct**. The right bar turns green. |
| Ask the same question to your next class | Click **Push again (fresh tally)**. Each push keeps its own results. |
| Look at an earlier class's results | Use the dropdown at the top right of the results panel. |
| Stop late submissions | **Close submissions** (you can reopen them). |
| Help a student with no laptop | Use the **quick-add** buttons under the tally to enter their answer. |
| Project the results | **Present mode** hides the question bank and your PIN buttons. |
| Step away from your computer | Click **Lock**. Your PIN unlocks it again. |

Multiple-choice answers are shuffled each time you push, so the correct answer isn't always A. Students also get a **"Submit for a classmate"** link, so a neighbor can enter an answer for someone without a laptop.

---

## If something goes wrong

The page shows a yellow **Heads up** box describing the problem. Here are the common ones:

- **"Can't find its firebase-config.js file"**: Step 5 didn't save. Check that the file has your values between the braces.
- **"Anonymous sign-in is turned off"**: Redo Step 6.2.
- **"Firebase doesn't recognize this website"**: Add your `yourname.github.io` address in Step 6.3.
- **"That PIN isn't right" when you type 1234 the first time**: The rules from Step 7 weren't published.
- **Forgot your PIN**: In Firebase, open **Firestore Database → Data**, then the **config** collection, and delete the **pin** document. The PIN goes back to 1234, and you'll choose a new one the next time you unlock.
- **Students see "Didn't send"**: Make sure a question is pushed and submissions are open.
- **Works at home but not at school**: Open the **Connection check** at the bottom of the page. If anything shows ❌, ask your tech department to allow `gstatic.com`, `firestore.googleapis.com`, and `cdn.jsdelivr.net`.

After any change on GitHub, wait about a minute and refresh.

---

## Good to know

- **Cost:** Firebase's free plan allows tens of thousands of submissions per day, far more than one teacher needs.
- **Privacy:** The tool never asks for student names or logins, and only you can read the responses. Responses older than 30 days are deleted automatically. Students can still type anything into a math answer box, so follow your school's policies.
- **About the PIN:** It keeps students out of the teacher view, but it isn't bank-level security. A longer PIN is safer, and you should never type it while projecting.
- **Getting updates:** If this project is improved later, a **Sync fork** button appears on your GitHub copy. Clicking it pulls in the new version, including any new stock questions, and keeps your own `firebase-config.js` and your edits.
- **Support:** This is shared as-is, as a free classroom project. Your copy is entirely yours to use and modify.

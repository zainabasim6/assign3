~~~{"variant":"standard","title":"README.md for Auto-Monitor Script","id":"72615"}
# Auto-Monitor Git Script

This project contains a Bash script that **monitors a folder for file changes**, automatically **commits and pushes changes to a GitHub repository**, and **sends email notifications** to collaborators via SendGrid.

---

## **Files in this project**

- `monitor_and_push.sh` — Bash script that monitors changes and automates Git + email.
- `config.cfg` — Configuration file with user-specific settings (paths, Git info, email info, SendGrid API key).
- `checksum.txt` — Stores checksums of files to detect changes.
- `src/` — Folder containing files to monitor.
- `README.md` — This documentation.

---

## **Prerequisites**

Before running the script, make sure you have:

1. **Git installed**  
   Check with:

   ```bash
   git --version
   ```

2. **Curl installed**  
   Check with:

   ```bash
   curl --version
   ```

3. **SendGrid account and API key**  
   - Create a free account at [SendGrid](https://sendgrid.com/)  
   - Go to **Settings → API Keys → Create API Key**  
   - Copy your API key and paste it in `config.cfg`

4. **A GitHub repository**  
   - Create a repository to test auto-commits  
   - Connect it to your local folder:

   ```bash
   cd /path/to/your/repo
   git init
   git remote add origin https://github.com/yourname/yourrepo.git
   git push -u origin master
   ```

---

## **Configuration (`config.cfg`)**

Edit `config.cfg` with your settings:

```bash
# Local repo path
REPO_PATH=/c/Users/hp/ssd/test-auto-repo

# Folder to monitor
WATCH_PATH=/c/Users/hp/ssd/test-auto-repo/src

# Git settings
GIT_REMOTE=origin
GIT_BRANCH=master

# Email settings
EMAIL_RECIPIENTS=your-email@example.com
SENDER_EMAIL=your-email@example.com
SENDGRID_API_KEY=SG.your_real_key_here

# Checksum file
CHECKSUM_FILE=$REPO_PATH/checksum.txt
```

---

## **How to run the script**

1. Make the script executable:

```bash
chmod +x monitor_and_push.sh
```

2. Run the script:

```bash
./monitor_and_push.sh
```

- On first run, it will create `checksum.txt` and check all files.  
- If changes are detected in any file in `src/`, it will:
  1. Update the checksum
  2. Commit and push to GitHub
  3. Send an email notification via SendGrid

---

## **Example usage**

1. Add a new line to a monitored file:

```bash
echo "Some new content" >> src/test.txt
```

2. Run the script again:

```bash
./monitor_and_push.sh
```

- Output will show:

```
Change detected in src/test.txt
Changes committed, pushed, and email sent.
Email sent successfully!
```

3. Check your inbox → email notification from SendGrid.

---

## **Error Handling**

The script handles common errors:

- Folder does not exist → exits with a message
- Git add/commit/push failures → prints error and continues
- SendGrid API errors → prints HTTP status code
- Empty folder → prints warning

---

## **Notes**

- Use your **real SendGrid API key** for testing email notifications.  
- Make sure the **sender email** is verified in SendGrid.  
- You can monitor any folder by changing `WATCH_PATH` in `config.cfg`.  
- `checksum.txt` keeps track of file fingerprints to detect changes accurately.

---

## **Author**

Zainab Asim  
FA22-BCT-038

~~~

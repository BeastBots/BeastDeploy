<div align="center">
<!-- <img src="https://i0.wp.com/gluonhq.com/wp-content/uploads/2018/05/heroku-logotype-vertical-purple.png" alt="Heorku Image" align="right" width="150">-->

# ***HEROKU DEPLOY GUIDE***

</div>

---

### 1️⃣ ***METHOD 1: (Github Workflow Guide)***

<details>
  <summary><b>Expand All Steps to Deploy <sup><kbd>Click Here</kbd></sup></b></summary>

**Step 1 :** Fork and Star the Repository

  - Click the **Fork** button at the top-right corner of this repository.
    > Star the repository to show your support.

**Step 2 :** Navigate to Your Forked Repository

- Access your forked version of the repository.

**Step 3 :** Enable `GitHub Actions` for your repo

- Go to the **Settings** tab of your forked repository.
- Enable **Actions** by selecting the appropriate option in the settings.

**Step 4 :** Run the Deployment Workflow to Deploy

  1. Open the **Actions** tab.
  2. Select the `Deploy to Heroku` workflow from the available list.
  3. Click **Run workflow** and fill out the required inputs:
     
   - **BOT_TOKEN**: Your Telegram bot token.
   - **OWNER_ID**: Your Telegram ID.
   - **DATABASE_URL**: MongoDB connection string.
   - **TELEGRAM_API**: Telegram API ID (from [my.telegram.org](https://my.telegram.org/)).
   - **TELEGRAM_HASH**: Telegram API hash (from [my.telegram.org](https://my.telegram.org/)).
   - **HEROKU_APP_NAME**: Name of your Heroku app.
   - **HEROKU_EMAIL**: Email address associated with your Heroku account.
   - **HEROKU_API_KEY**: API key from your Heroku account.
   - **HEROKU_TEAM_NAME** (Optional): Required only if deploying under a Heroku team account.
   - **UPSTREAM_REPO**: Upstream Repo of your Fork or Main Repo
     
  4. Run the workflow and wait for it to complete.


**Step 5 :** Finalize Setup of your bot

- After deployment, check logs in your Heroku dashboard, If problem, Reach to Support Group.
- Use the `/bsettings` command to upload sensitive files like `token.pickle` if needed as well as all the important Variables within it.
  > **NOTE** : Don't Add any Other variable except the Variables mentioned here.


</details>

---

### 2️⃣ ***METHOD 2: (Heroku CLI Guide)***

<details>
  <summary><b>Expand All Steps to Deploy <sup><kbd>Click Here</kbd></sup></b></summary>

**Step 1 :** Git clone this Repo and change directory
> Make sure git is Installed in your system or quick run `apt-get install git pip curl -y`

```shell
git clone https://github.com/BeastBots/BeastDeploy deploy && cd deploy
```

**Step 2 :** Now Install Heroku in your Sytem or checkout Official Heroku Deploy Docs, or Download via `apt-get` or `npm`
> For Android : Use `termux` (Download via FDroid) for CLI usage

**The script requires sudo and isn’t Windows compatible.**
```shell
curl https://cli-assets.heroku.com/install.sh | sh
```

**Install with Ubuntu / Debian apt-get**
```shell
curl https://cli-assets.heroku.com/install-ubuntu.sh | sh
```

**Install via `npm` (Not Recommanded)**
```shell
npm install -g heroku
```

**Official Heroku Install Guide :** [Check Here](https://devcenter.heroku.com/articles/heroku-cli#install-the-heroku-cli)

**Step 3 :** Login into Heroku and Log In CLI via Browser 

_With Browser_
```shell
heroku login
```

**OR**

_Without Browser_
```shell
heroku login -i
```

- Put `Heroku Email` : Heroku Email `email@example.com`
- Put `Heroku Password` : Heroku API Key. Get from [Here](https://dashboard.heroku.com/account)

**Step 4 :** Create Heroku App and specify stack and region with App Name

```shell
heroku create --region eu --stack container APP_NAME
```

**To Be Noted**: Copy the `BASE_URL` after the App is Created and Put the Value in `BASE_URL` when editing `config.py`

**Notes:**
- `--region eu` for Europe Server.
- `--region us` for United States Server.
- `APP_NAME` should be replaced with your unique app name _(Optional)_. If not given it generates a random name.
- `--stack container` for setting stack to container for Dockerfile.
- `--buildpack heroku/python` for using build slug for repo deploy and build.

**Step 5 :** Now set all the Required Variables and Files into this Branch MAIN Repo like config.py, accounts.zip, token.pickle, All Private Files(optional)- 
  > Only config.py Mabdatory with Only Mandatory Vars Only, After that Put all Private Files or Vars via Bot Settings `/bs`

**To Edit Inside CLI (nano Editor):** _(Termux Users)_
```shell
nano config.py
```
- **Sample config.py** _(Copy these and Paste in Editor and Fill Up)_
  ```
  BOT_TOKEN = ""
  TELEGRAM_API = 0
  TELEGRAM_HASH = ""
  OWNER_ID = 0
  UPSTREAM_REPO = ""
  UPSTREAM_BRANCH = "master"
  DATABASE_URL = ""
  BASE_URL = ""
  ```
- After Setup Save from Editor via `CTRL + O` and `Enter`, followed via `CTRL + X` !

**Helpful Commands:**
- **Exit from nano** : `CTRL + X`
- **Save File** : `CTRL + O`
- **Check Help** : `CTRL + G`
- **Undo Changes** : `ALT + U`
- ^ means CTRL _(Termux Users)_

**Step 6 :** Set Local git remote for Heroku. Give All Commands One by One.

```shell
git add . -f
git commit -m "HK Setup"
heroku git:remote -a APP_NAME
```

**Step 7 :** Now push to Heroku via git forcefully to build.

```shell
git push heroku main -f
```

**Heroku Logs:** When checking Logs, Use this will give Complete Logs.
```shell
heroku logs -a APP_NAME -t
```

- Add arg `-t` for Live Stream Logs and Use `CTRL + C` to Exit from it.

**All Heroku CLI Commands :** [Click Here](https://devcenter.heroku.com/articles/heroku-cli-commands#heroku-config-set)

</details>

---

### 🔠 ***Variables Description:***

<details>
  <summary><b>View All Variables <sup><kbd>Click Here</kbd></sup></b></summary>

- `BOT_TOKEN`: Telegram Bot Token that you got from [BotFather](https://t.me/BotFather). `Str`
- `OWNER_ID`: Telegram User ID (not username) of the Owner of the bot. `Int`
- `TELEGRAM_API`: This is to authenticate your Telegram account for downloading Telegram files. You can get this from <https://my.telegram.org>. `Int`
- `TELEGRAM_HASH`: This is to authenticate your Telegram account for downloading Telegram files. You can get this from <https://my.telegram.org>. `Str`
- `BASE_URL`: Valid BASE URL where the bot is deployed to use torrent web files selection. Format of URL should be `https://app-name-random_code.herokuapp.com/`, where `app-name` is the name of your heroku app Paste the URL got when the App was Made. `Str`
- `DATABASE_URL`: Database URL of MongoDb to store all your files and Vars. Adding this will be Helpful. `Str`
- `UPSTREAM_REPO`: GitLab repository URL, if your repo is private add `https://<deploy_token>:<password>@gitlab.com/<your_username>/<repository_name>` format. `Str`.
    - **NOTE**: Don't forget to remove '<' and '>'. To generate gitlab Deploy Token. Follow [This](https://docs.gitlab.com/ee/user/project/deploy_tokens/#create-a-deploy-token)
        - Any change in docker you need to deploy/build again with updated repo to take effect. 
        - **No Need to delete .gitignore file or any File**
- `UPSTREAM_BRANCH`: Upstream branch for update. Default is `wzv3`. `Str`

</details>

---

### ⚠️ ***Branch Specifications:***

- All files to be Uploaded in this `main` Branch and set Upstream as `master` Branch of actual repo.

---

### ❤️ ***Credits:***
- [Beast Bots](https://github.com/BeastBots)
- [Silent Demon SD ( MysterySD )](https://github.com/SilentDemonSD)
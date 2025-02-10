## Troubleshooting
Below is a list of issues and fixes.

## `cd ~/Desktop` does not work on Windows
1. Windows introduced OneDrive, which moved the Desktop folder to a different location `~/OneDrive/Desktop`.
2. To go to the Desktop in your command line, run `cd ~/OneDrive/Desktop`.

## Git no longer supports password when using `git push`
1. When running `git push origin master` or `git push origin main` when entering your password, you may get this error even if your password is correct:
```
remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.
fatal: Authentication failed for 'https://github.com/username/repository/'
```
- Github no longer allows using a password to access it.
- **Note:** if you're using Windows, running `git push ...` might open a popup asking you to log into Github. If so, click the button to sign in with browser, sign in to Github, and click Authorize.
- If the above does work or no popup appears, read the troubleshooting steps below.

2. Instead of entering a password, we need to enter an access token.
3. To create an access token, go to your Github account in the browser.
4. Click your profile picture in the top-right, and click "Settings".
5. On the left, scroll down and click "Developer settings".
6. On the left, click "Personal access tokens", and click "Fine-grained tokens".
7. Click "Generate new token".
8. Set a Token name, Expiration = 30 days, Repository access = all repositories.
9. Open "Repository permissions", scroll down to "Contents", and change the Access to "Read and write".
10. Scroll to the bottom and click "Generate token"
11. Github will give you an access token like this:
```
github_pat_11AY7DDYA0TJg09BH... (it's long)
```
12. Copy this access token and put it in a safe place (don't share this since it can give anyone access to your Github).
13. Run `git push ...` again and when it asks for a password, paste the access token you created, press Enter.

### If using the access token did not work
1. Try running `git remote remove origin`
2. Run `git remote add origin https://<username>@github.com/<username>/<repository>.git` (replace `<username>` with your github username and `<repository>` with the name of your repository).
3. Git should ask for a password. Paste the access token you created earlier, press Enter.

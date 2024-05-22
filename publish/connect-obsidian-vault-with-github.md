---
title: "The Easiest Way to Connect Your Obsidian Vault with Github"
---
I watched a few videos on how to setup the obsidian-git plugin and it feels like most of them overcomplicate the process. So I decided to write a set of instructions and a video to show how easy it to accomplish this even if you have no idea what "git" is.

By the end of this tutorial, you will be able to sync your notes from Obsidian to Github for free!

[https://youtu.be/5YZz38U20ws](https://youtu.be/5YZz38U20ws)

1. Create a repository or [[publish-your-obsidian-notes-with-linked-blog-starter|fork the md repo]] in github
2. [Download Git](https://git-scm.com/downloads)
3. Create a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-personal-access-token-classic) from github
![[create-pat-github.png]]
5. Install the [Obsidian Git](https://github.com/denolehov/obsidian-git/wiki/Installation) community plugin
6. Create a folder to store the repository. (e.g. `remote-blog/`). Set scopes to repo & expiration to no expiration
7. Run the command (CMD/Ctrl + P):  `Clone an existing remote repo`
![[clone-repo-git-plugin.png]]
5. Paste the URL of the forked repository in the following format
```
https://<PERSONAL_ACCESS_TOKEN>@github.com/<USERNAME>/<REPO>.git
```

For example it might look like this:
```
https://ghp_XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX@github.com/ithinkwong/linked-blog-starter-md.git
```
7. Then type in the folder you created in step 5 (e.g. `remote-blog/`)
8. Restart Obsidian
9. Make edits to your notes
10. Publish your notes run the command "Obsidian Git: Create backup" by opening the command palette (CMD/Ctrl + P)
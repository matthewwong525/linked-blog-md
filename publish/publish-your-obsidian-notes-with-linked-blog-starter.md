---
title: "Publish your Obsidian Notes with linked-blog-starter"
---
By the end of this tutorial, you'll have a github repository that will automatically publish notes to your custom website everytime you upload new notes to the `publish` folder.

Video: https://www.youtube.com/watch?v=rKSpK1dXn4E

## Step-by-step instructions to setup your blog

1. Fork the repository [linked-blog-starter-md](https://github.com/matthewwong525/linked-blog-starter-md) repository. This repository is where the publishing occurs
![[fork-linked-blog-starter-md.png]]
2. Create a [Vercel](https://vercel.com/dashboard) account then go to your dashboard then (Add New... > Project)
3. Import the repository you just forked
4. In the "Configure Project" settings (before you deploy), **set the "Framework Preset" to Next.JS** . Then click the "Deploy" button.
![[configure-project-vercel.png]]
5. After clicking the Deploy button, you'll see that the deploy failed. That's as expected.
6. OPTIONAL: Go to your [dashboard](https://vercel.com/dashboard), then click on the project you created and disconnect the git repository (Settings > Git > Disconnect)
![[disconnect-repo-vercel.png]]
7. Then, [[get-project-id-account-id-and-token-vercel|get the account id, project id and token from vercel]]
8. Now with the account id, project id, and token, go back to your forked repository and update Github secrets (Settings > Secrets > Actions). Add the following secrets: `VERCEL_ORG_ID`, `VERCEL_PROJECT_ID`, `VERCEL_TOKEN`
![[github-secrets-vercel.png]]
9. Finally, click "Actions", and enable the workflow
![[enable-actions-github.png]]
10. Now whenever any notes are uploaded to the `publish` directory of the repository, they are automatically published online! You can find the domain in Vercel under `Projects`.

**Note**: Make sure you don't delete the `/publish/home.md` file as that is your "landing page"

Optionally, you can:
- [[connect-obsidian-vault-with-github|Publish Notes within your Obsidian Vault]] by installing the Obsidian Git plugin
- [[update-publish-settings-github-actions|Update the publish settings]] to publish your notes to a [[deploy-a-custom-linked-blog-starter|custom version]] of the linked-blog-starter 
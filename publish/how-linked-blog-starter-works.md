---
title: "How the Linked Blog Starter works"
date: 2022-12-30
---
1. Notes are updated in your Obsidian Vault
2. The [Obsidian Git](https://github.com/denolehov/obsidian-git) plugin pushes the notes to the remote repository. With the following command: `Obsidian Git: Create backup`
3. A [github action](https://github.com/matthewwong525/linked-blog-starter-md/blob/main/.github/workflows/publish.yml) is automatically triggered to deploy the notes using a [specified template](https://linked-blog-starter.vercel.app/deploy-a-custom-linked-blog-starter)

![[how-linked-blog-starter-works.png]]
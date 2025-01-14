---
title: "Update the Publish Settings"
---
There are two things you can modify in the workflow. The publish directory and the blog repository.

- `BLOG_REPO`: Next.JS app repository template that is used to publish your markdown notes. This is useful when you [[deploy-a-custom-linked-blog-starter|create your own custom linked blog]]
- `PUBLISH_DIR`: The folder that is published to the linked blog. All files and attachments in this folder will be published on the web

Go into `.github/workflows/publish.yml` in your forked repository forked from [linked-blog-starter-md](https://github.com/matthewwong525/linked-blog-starter-md) and update the environment variables to your desire
![[publish-dir-yml.png]]
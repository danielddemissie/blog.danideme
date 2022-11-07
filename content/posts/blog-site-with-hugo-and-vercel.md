---
title: "Blog Site With Hugo and Vercel"
date: 2022-11-07T09:19:10+03:00
tags : ["hugo","vercel"]
draft: false
---

![hugo-vercel](https://i.ibb.co/51BSJGc/image-2022-11-07-131127067.png)
# Hello friends, This my step by step guide to build and deploy blog site with `Hugo` and `Vercel` that I used for my blog site and I hope this might be some use for you too.


### 1. Install Hugo
Installing Hugo on Linux.
If your distribution support `snap`

```bsh
snap install hugo --channel=extended
```

Or you can use `apt-get`

```bash
sudo apt-get install hugo
```
Check if hugo is successfully installed.

```bash
hugo version
```
If you get a response similar Hugo is successfully installed.
```bash
hugo v0.105.0-0e3b42b4a9bdeb4d866210819fc6ddcf51582ffa+extended linux/amd64 BuildDate=2022-10-28T12:29:05Z VendorInfo=snap:0.105.0
```
If you are using windows follow this instruction [hugo-windows](https://gohugo.io/getting-started/installing/#windows)

### 2.Create new Site
After installing Hugo lets create our blog site

1. Open up your terminal.
2. `cd` to your prefered directory to work.
3. Create new Hugo site with your blog site name

```bash
hugo new site blog-site
```

This will give us short command on how to add a theme , content and commands to build site we will see all of the later.

```
Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

### 3.Use Hugo theme

Hugo has nice configuration to add our preferd them and manage the UI/UX of our site. once yout select a [Hugo-Themes](https://themes.gohugo.io/)
we can add the theme to our site using one of these two methods.

1. Make the selected theme git repository a `subtree` to our site
    * if want to follow the change to the parent and update accordingly.

2. Manually download the theme git repository and unzip it in our site under `theme` directory or use `git clone`.
    * use this approach if you are satisfied with the current change and doesnot intend to follow the change of the parent (theme) repository.


For our site lets use [m10c](https://github.com/vaga/hugo-theme-m10c.git) theme again we have two option to use this theme.
Since I'm fine with current UI/UX and functionality of the theme and i want store the file localy i will the seccond approach if you want to.

clone the theme 
```bash
cd themes
git clone https://github.com/vaga/hugo-theme-m10c.git ./m10c
```

### 4.Update the config.toml

Now we have to tell the config.toml file

    * the theme used
    * about the author of the blog
    * available menus
    * social media links and more

1.Open up your config.toml file and add this information
 `Remember to change the data to your own information.`

```bash
languageCode = "en-us"
title = "Daniel's Blog"
theme = "m10c"

[[menu.main]]
  identifier = "tags"
  name = "Tags"
  url = "/tags/"
  weight = 2
  
[[menu.main]]
  identifier = "home"
  name = "Home"
  url = "/"
  weight = 1

[params]
  author = "Daniel Demelash"
  description = "The little things I know about software development."
  avatar = "images/profile_pic.png"
  #add avatar image
  menu_item_separator = "|"
  favicon = "images/favicon.ico"
  #add favico image
  
  [[params.social]]
    icon = "github"
    name = "GitHub"
    url = "https://github.com/danielddemissie"

  [[params.social]]
    icon = "linkedin"
    name = "Linkedin"
    url = "https://linkedin.com/in/danielddemissie"

  [[params.social]]
    icon = "twitter"
    name = "Twitter"
    url = "https://twitter.com/danielddeme"

 

```

For this to work properly you have to add `favico` and the `avatar` image inside public/images folder and static/images folder with same file name.

### 5. Create first post

Now it's time to add our first blog to our site to do this first go back to main directory and run this command.

```bash
cd ..
hugo new posts/first-post.md
```
This command posts directory with `first-post.md` inside the content folder.When you open the `fist-post.md` file in text your editor you will see that the post is in a draft mode or `darft = true` so add some content to this file and change `draft = false` after doing that save your changes and run these commands.

```bash
hugo 
hugo server
```
The `hugo` command will generate the neccessary configuration and html files to render the app.
```
Start building sites … 
hugo v0.105.0-0e3b42b4a9bdeb4d866210819fc6ddcf51582ffa+extended linux/amd64 BuildDate=2022-10-28T12:29:05Z VendorInfo=snap:0.105.0

                   | EN  
-------------------+-----
  Pages            | 10  
  Paginator pages  |  0  
  Non-page files   |  0  
  Static files     |  1  
  Processed images |  0  
  Aliases          |  2  
  Sitemaps         |  1  
  Cleaned          |  0  

Total in 94 ms
```

`hugo server` will start up the application at port 1313.
if no other service is running on that port. Now that our blog site is  up and running lets open http://localhost:1313 in our browser.

### 6. Push to gitHub
Create new github repository with the site name and copy your the url.
The only reason i rename the main branch from `master` to `main` is I like main better unlike github's reason.

```bash
git init
git add -A
git commit -m "START: first commit"
git branch -M main
git remote add origin https://your-github-account/site-name.git
git push -u origin main
```

### 7. Deploy to vercel

Vercel is the platform for frontend developers, providing the speed and reliability innovators need to create at the moment of inspiration.Beside that They offer one of the best Hobby(Free) account service.

![vercel-limit](https://i.ibb.co/XZn2z3T/image-2022-11-07-105121043.png)

If you don't have vercel account,create free vercel account and come back here!.

To deploy Hugo sites to vercel doesnot require any additional configuration all you have to do is just push the change you want to deploy to main/master of the project repository and vercel will do the its own configuration for Hugo site.

Lets deploy. first check If everything is saved then

```bash
git add .
git commit -m "DEPLOY: deploy to vercel"
git push
```
open your vercel dashboard
#### Add new project
![add-new-project](https://i.ibb.co/SrXtrsP/Screenshot-from-2022-11-07-11-07-22.png)

#### Import from github
![import-from-github](https://i.ibb.co/TtbbNYs/Screenshot-from-2022-11-07-11-07-41.png)

#### Select the project to deploy and click deploy.
![select-the-project-to-deploy-and-the-click-deploy](https://i.ibb.co/sV7XfLt/Screenshot-from-2022-11-07-11-07-58.png)

#### Congrats 🎉 your blog site is LIVE!.
![deployed](https://i.ibb.co/TTPvHVF/image-2022-11-07-122304084.png)



Now whenever you made some change to the `main` branch vercel will update your site.

**Thanks** for reading my blog.

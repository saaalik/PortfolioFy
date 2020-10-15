<div align="center">
<h1 align="center">Ultimate Portfolio Maker</h1>
<h3 align="center">Dynamically Self Updating Portfolio</h3>
<h4 align="center"> Developed by: Kaustubh Gupta </h4>
<img src="./images/preview.PNG" alt="Screeenshot taken on 11th October, 2020" align="center">
</div>

As a developer we create hundreds of repositories and hardly 15-20 of them actually make it to final project we deploy and showcase on social media/linkedin. This GitHub action allows you to generate your perfect self updating portfolio with Projects, Hackathons and latest Blogs (optional). An index file is generated by this action which with the help of GitHub pages gets deployed as soon as it is commited the repository. If you write blogs, then you can integrate [Blog Post Workflow](https://github.com/marketplace/actions/blog-post-workflow) in our workflows to update latest blogs in your portfolio. Let's see how to setup this action

## Important note
- The repositories need to have "project" topic to add them in project section and "hackathon" topic to add them in hackathon section. If you add both the topics to same repository then it will reflected in both sections!
- You only need to have a GitHub personal access token which can be obtained by going to Settings > Developer Settings > Personal Access Tokens. Generate a new token and give atleast give this much permisions:
<div align="center"> <img src="./images/config.PNG" align="center"> </div>

*Note: If you give personal repositories access then they will be added to the sections but their links will not work*

## Installation

Create a new folder called  `.github/workflows/update.yml`, file name is your choice. Paste the following starter code:

```yml
name: Latest portfolio
on:
  schedule:
      # Runs at the end of every day. You can customise according to your need. You can also trigger this action for other events. Check github actions page for that.
      - cron: '0 0 * * *'
  workflow_dispatch:

jobs:     
  job_1:
    name: update-index-with-project
    runs-on: ubuntu-latest
    steps:
        - uses: actions/checkout@v2
        - uses: kaustubhgupta/PortfolioFy@v1.0
          with:
            gh_token: ${{ secrets.TOKEN }} # Create a secret for access token and modify the name as you wish
  
        - uses: test-room-7/action-update-file@v1
          with:
            file-path: |
              index.html
            commit-msg: index file added
            github-token: ${{ secrets.TOKEN }}
```

## Usage
This action generates a index.html file which is website ready. Simply enable the GitHub pages to deploy the index file and boom, you have your portfolio which self updates when you add your projects or hackathons projects!

## Add Blogs updatation
There is an action called [Blog Post Workflow](https://github.com/marketplace/actions/blog-post-workflow) which updates latest blogpost on schedule. You can easily integrate this in your workflow via this method: (I highly recommend to use this!)
```yml
name: Latest blog post workflow
on:
  push:  # Everytime index.html is pushed, this action runs and updates the blogs section!
    
jobs:
  update-readme-with-blog:
    runs-on: ubuntu-latest
    steps:
        - uses: actions/checkout@v2
        - uses: gautamkrishnar/blog-post-workflow@master
          with:
            feed_list: <Your feedlist>
            max_post_count: 7
            readme_path: index.html
            template: "$newline <h2 class='h2-blog'><a class='a-lightblue' href=$url>$title</a></h2>$newline <br>"  # Do not change the template as it will not render good results!
            gh_token: ${{ secrets.TOKEN }}

```

*Do star the repository! It gives me motivation to develop more projects like this!*

## Special Mentions
A special thanks to:
- [Anurag Hazra](https://github.com/anuraghazra/github-readme-stats) for creating readme stats vercel app which is being used for GitHub Stats Image.
- [Gautam krishna R](https://github.com/marketplace/actions/blog-post-workflow) GitHub action which makes it possible to update blogpost.
- [Rajveer Narag](https://github.com/RajveerN01) for helping out with front-end developement and mobile view optimization.
- [Test Room 7](https://github.com/marketplace/actions/update-files-on-github) GitHub action which enables commit of files to repository
- [GitHub actions](https://docs.github.com/en/free-pro-team@latest/actions) docs, it's the best guide!

*Create blogs, videos and tag me! I will definately have a look and featue them here!*

## Featured Content
- [Github Action That Automates Portfolio Generation](https://towardsdatascience.com/github-action-that-automates-portfolio-generation-bc15835862dc) - Medium Blog

## License
[MIT](https://choosealicense.com/licenses/mit/)

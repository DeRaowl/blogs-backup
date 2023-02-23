# GitHub Actions Basics

Automation is a key part of modern DevOps practices, allowing software development teams to quickly and efficiently develop, test, and deploy software. GitHub Actions is a powerful automation platform that can be used to automate tests, builds, and deployments.

With GitHub Actions, developers can create custom workflows to integrate with existing processes and automate their workflow from code to deployment.

## Prerequisite

Though we will start exploring GitHub actions from the beginning. It is good to have some Basic understanding of,

* GitHub
    
* YAML(Yet Another Markup Language)
    

By the end of this post, you will be able to write a simple workflow which triggers whenever a user creates an issue in GiHub and it will auto-assign to the specified user.

## So what are GitHub Actions?

In simple terms, GitHub Actions is a way to make your computer do things automatically. For example, you can make your computer check your code for errors every time you make a change, or you can make it automatically create a new version of your project when you're ready to share it with others. It's like having a robot helper to help you with your projects!

# GitHub actions and its components

Before diving into creating workflow and actions it is good to know the key concepts involved in creating them.

## 1\. Workflow

GitHub workflow is a configurable automated process defined by a YAML file that will run when any event is triggered in your repository.

Workflows are defined in the `.github/workflows` directory in a repository.

## 2\. Events

GitHub Events are special triggers that can cause a workflow to run. For example, when someone pushes a change to a repository, that can trigger a workflow to run.

GH Actions are event-driven, which means you can define what happens after a specific event.

## 3\. Jobs

GitHub Jobs are the individual tasks that make up a workflow. A job is a set of steps that run on the same runner.

[![GitHub Jobs.](https://cdn.hashnode.com/res/hashnode/image/upload/v1677122528034/21bef07e-19fe-4dda-a842-f0d357b1ae0d.webp align="center")](https://www.macstadium.com/blog/sharing-variables-between-jobs-in-github-actions)

## 4\. Steps

Steps are individual tasks that can run commands, such as a shell command or an action, in a job within a workflow.

## 5\. Action

Actions are the commands that define the steps of each job. They are combined into steps to create a job. Actions are standalone commands that can be portable.

# Magic of Workflow:

Now we have a high-level understanding of different components, let us write and customize our first workflow.

First and foremost we need a `.yml` file to create our workflow.

> All workflow files related to GitHub Actions must live in the .github/ workflows directory and must have either the .yml or .yaml file extension.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677123430040/1d9585dc-f4a3-4fbe-b08c-30d7e32b143b.png align="center")

Note: [gh-actions](https://github.com/DeRaowl/gh-actions) is my repository name created. You can name it as per your choice.

## First Workflow

```yaml
name: GH Actions
on:
    issues:
        types: [opened]
jobs:
    auto-assign:
        runs-on: ubuntu-latest
        steps:
            - name: 'Auto-assign PR'
              uses: pozil/auto-assign-issue@v1
              with:
                  assignees: deraowl
                  repo-token: ${{ secrets.GITHUB_TOKEN }}
```

Don't worry about the weird syntax, it is a YAML code and I will explain every line in-depth. So no worries :)

Specific keys that can be added to the workflow:

1. name:
    
    * We need to provide a meaningful full name as it will be visible on the actions tab in the GitHub repository.
        
    * As it is an optional field, If you do not add this key and a corresponding value, GitHub will set the name of your workflow to the file path relative to the root of the repository.
        
2. on:
    
    * This mandatory key specifies which event or events will trigger the workflow.
        
    * This accepts a single event or an array of events.
        
3. jobs
    
    * Workflow runs can have one or more jobs.
        
4. job\_id
    
    * Each job defined must have the job\_id associated with it.
        
    * Each job ID must start with either an underscore (\_) or with a letter and must be unique to that specific job.
        
5. runs\_on
    
    * It is a required field, that specifies the type of machine that the job will run on.
        
    * In our case, we are using ubuntu-latest as a virtual environment.
        
6. steps
    
    * Steps are tasks that exist within a job. They can contain a series of tasks and run commands, set up tasks, or run an action.
        

<mark>To Summarize the above workflow,</mark>

The Issue assignment workflow will run every time an issue is opened. This will trigger a job called auto-assign, which will run on the latest version of Ubuntu, running on a GitHub-hosted runner.

The step within the job will use an action called Auto-assign issue, which can be found in GitHub Marketplace. This step will use a repository token (GITHUB\_TOKEN), which is automatically created when GitHub Actions are enabled in a repository. Finally, the job will assign an assignee – in this case, deraowl – to the newly created issue.

## Trigger the Workflow

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677125082353/91bd706e-0190-4a0c-9af1-f0c709b6f8a5.png align="center")

To trigger the above-created workflow just open a new issue under the same repository and click on Submit a new issue. And that's it.

It will trigger the workflow which is mentioned above

If your workflow fails due to a `For resources not accessible by integration`, go to `github.com/username/repository/actions` and under the general section change Workflow permission to Read and write permissions. This should resolve the

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677125297004/c7a04bff-4e36-411e-99f8-4fe39c9d2705.png align="center")

## Check Actions Live

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677125513850/145eb48b-2148-4a6f-8f79-0070f7b37b22.png align="center")

Now navigate to the Actions section in the header. Here you can see the job `auto-assign` which will be executed successfully. It is a simple job created which will start executing as soon as an issue has been created.

This can be used to auto-assign the assignee or auto-create specific labels. We will explore multiple jobs and actions in upcoming posts.

Now if you check the issue which we created earlier named `GH actions testing` under the Assignees section is now assigned to DeRaowl which is me.

This name we defined in the job under `assignees`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677125765679/28d32807-f0b4-402c-8220-aa5f7f3fada1.png align="center")

# And it's a wrap

So that's it. How easy it is to create a workflow. In upcoming posts, we will explore and create much more complex jobs and also will explain how we can create our job as `auto-assign` and publish it to GitHub marketplaces.

You can check out my [Repositor](https://github.com/DeRaowl/gh-actions)y for the code. And if you want to explore more about GitHub actions then GitHub has very good Documentation.

---

# References

* [https://docs.github.com/en/actions](https://docs.github.com/en/actions)
    
* [https://github.com/marketplace/actions/auto-assign-issue](https://github.com/marketplace/actions/auto-assign-issue)
    
* [https://lo-victoria.com/series/github-actions](https://lo-victoria.com/series/github-actions)
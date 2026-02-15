# 1:

1. https://github.com/fleeshka/DevOps-Intro/actions/runs/22035534716
![successful pipeline](image.png)

2. From this quickstart, I learned that GitHub Actions uses jobs (like "Explore-GitHub-Actions") which are sets of steps that run on a virtual machine called a runner (ubuntu-latest), and these workflows are automatically triggered by events such as triggers (like on: [push]). The steps can execute shell commands, check out repository code using actions like actions/checkout, and use contextual variables like ${{ github.event_name }} to access information about the workflow run.

3. A push event to the repository triggered the workflow run.

4. The workflow execution process begins when a push event triggers the workflow, which then launches a job on an Ubuntu runner that sequentially executes each step, including running echo commands, checking out the repository code with actions/checkout, and listing files in the workspace.

# 2:

1. Added a 
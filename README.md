# test_github_action

## To run workflow

1. Navigate to the Repository: Go to the main page of your GitHub repository in a web browser.

2. Actions Tab: Click on the "Actions" tab at the top of your repository page. This tab is where you can access and manage your workflows.

3. Trigger Workflow Based on Events:If the workflow is configured to run on specific events (e.g., push to a branch or pull request), you don't need to manually trigger it. It will automatically start when the specified event occurs.

4. Monitor Workflow Progress: After triggering the workflow, you can monitor its progress in the Actions tab. You'll see a new workflow run listed with details on its status, jobs, and steps.

5. View Workflow Details: Click on the workflow run you triggered to see more details, including the status of individual jobs and steps. This is where you can view the logs and results of the workflow.

6. Troubleshoot and Address Issues: If the workflow encounters errors or issues, review the logs and follow the error messages to diagnose and address the problems. You may need to make changes to your code or workflow configuration.

7. Repeat as Needed: You can trigger workflows manually whenever necessary or let them run automatically based on configured events. Make sure your workflow is achieving the desired outcomes for your project.



## The explanation for the code

     name: first-workflow

name: This is the name of the GitHub Actions workflow. In this case, it's named "first-workflow."

    on: [push]
    
on: Specifies the GitHub events that trigger this workflow. In this example, the workflow is triggered only when there is a push event to the repository. This means that it will run whenever code is pushed to any branch of the repository.

    jobs:
     check-python-version:

jobs: Defines a list of jobs that should be executed as part of the workflow. In this workflow, there is one job named "check-python-version."

    runs-on: ubuntu-latest

runs-on: Specifies the type of runner environment where this job will be executed. In this case, it's configured to run on the latest version of the Ubuntu environment provided by GitHub Actions.

    steps:

steps: Contains a list of steps that define the tasks to be performed as part of this job.

    - uses: actions/checkout@v3

uses: This step uses the actions/checkout@v3 action to check out the code from the repository. It fetches the latest version of your code so that subsequent steps can work with it.

    - name: Set up Python 3.10.12
      uses: actions/setup-python@v4
      with:
        python-version: 3.10.12

name: Assigns a name to the step for identification purposes.

uses: Utilizes the actions/setup-python@v4 action to set up a specific version of Python, in this case, Python 3.10.12, within the runner environment.

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install flake8
        pip install pylint
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
 
name: Names the step.
 
run: Contains a shell script that runs within the runner environment. This script performs several tasks:

Upgrades pip to the latest version.

Installs the Flake8 and Pylint packages using pip.

Checks if a "requirements.txt" file exists and, if so, installs the dependencies listed in that file.


      - name: Lint with flake8
        run: |
          flake8 src --count --select=E9,F63,F7,F82 --show-source --statistics
          flake8 src --count --max-complexity=10 --max-line-length=79 --statistics

name: Names the step.

run: Executes linting using Flake8 on the "src" directory. It performs two linting runs with different options:

The first run checks for specific error codes (E9, F63, F7, F82) and generates statistics and source code annotations.

The second run checks for maximum code complexity (10) and maximum line length (79), also generating statistics.

      - name: Lint with Pylint
        run: |
          pylint src

name: Names the step.

run: Executes linting using Pylint on the "src" directory.

## Output

![Screenshot from 2023-09-01 14-04-21](https://github.com/Triptiskillz/test_github_action/assets/63160367/3b949208-d156-4c17-a2ab-208213de2d46)

## Resource

Link: https://medium.com/swlh/enhancing-code-quality-with-github-actions-67561c6f7063

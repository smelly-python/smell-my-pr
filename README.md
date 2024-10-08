# Smelly Python: Smell My PR

An action that runs [`smelly-python`](https://github.com/smelly-python/smelly-python) and post summaries of present code smells to jobs and to PRs. Smelly Python runs `pylint` to check code smells present in your code. This action then posts a job summary in the Actions tab and a comment on your PR (if you pushed to a branch that has an open PR). 

<img width="796" alt="smelly-python's PR comment" src="https://user-images.githubusercontent.com/45203765/173336731-4b285432-3878-4dd8-bb49-d422dd81060e.png">

## Workflow setup

**Required input:**

- `command`: command that runs `smelly-python` on the module you want to analyse. We automatically install smelly-python using pipenv so you can use `pipenv run smelly-python -d <module>`. 
- `github-token: ${{secrets.GITHUB_TOKEN}}`

**optional input:**
- `install-pipenv` (Default True): Installs pipenv before trying to install smelly-python. Only set this to False when you have manually installed pipenv earlier.  

It is necessary to include the following permissions in your job. See the example of a workflow setup below.

```(yaml)
permissions:
  checks: write
  pull-requests: write
  contents: read
```

**Example:**

```(yaml)
jobs:
  linter:
    [...]
    permissions:
      checks: write
      pull-requests: write
      contents: read
    steps:
    - uses: actions/checkout@v3
    [...]
    - uses: smelly-python/smell-my-pr@main
      with: 
        github-token: ${{secrets.GITHUB_TOKEN}}
        command: pipenv run smelly-python -d src
        install-pipenv: true
```

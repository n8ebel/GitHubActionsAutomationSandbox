![Nightly Build](https://github.com/n8ebel/GitHubActionsAutomationSandbox/workflows/Nightly%20Build/badge.svg)

Example repo demonstrating different types of automated tasks and CI integrations

## Examples Included
- Simple GitHub Actions workflow examples
- ktlint running in CI
- Gradle task to copy a pre-push git hook that validates ktlint
- .gitignore file which allows code styles, scopes, templates, etc to be tracked
- Pull Request template for GitHub
- Bug Report & Feature Issue templates for GitHub
- Danger integration to report APK size
- Danger integration to warn if WIP
- Danger integration to thank PR author
- Danger integration to add inline ktlint issue comments
- Danger integration to warn about missing PR description
- GitHub Actions workflow to check for dependency updates every day at 8:00
- GitHub Actions workflow to parse PR number to be used when notifying of PR approval

## Triggering Repository_Dispatch Workflows

Running the following curl command will trigger 2 different workflows:
- `triggered_example.yml`
- `triggerable_tasks.yml`

```
curl -H "Accept: application/vnd.github.everest-preview+json" \
    -H "Authorization: token <your-token-here>" \
    --request POST \
    --data '{"event_type": "do-something"}' \
    https://api.github.com/repos/n8ebel/GitHubActionsAutomationSandbox/dispatches
```

With this command, the `triggerable_tasks.yml` workflow will run, but several of the steps will not run because the repository_dispath event didn't have the required properties passed with it.

To run the full `triggerable_tasks.yml` workflow, run the following curl command:

```
curl -H "Accept: application/vnd.github.everest-preview+json" \
    -H "Authorization: token <your-token-here>" \
    --request POST \
    --data '{"event_type": "do-something", "client_payload": { "text": "a title"}}' \
    https://api.github.com/repos/n8ebel/GitHubActionsAutomationSandbox/dispatches
```

## Triggering Workflow_Dispatch Events

Workflows configured to run in response to `workflow_dispatch` events may be triggered in 2 ways:
- using the GitHub Actions api
- from the GitHub Actions UI in your repository

To trigger the `workflow_dispatch_example.yml` workflow, the following curl can be used:

```
curl -H "Accept: application/vnd.github.everest-preview+json" \
    -H "Authorization: token <your-token-here>" \
    --request POST \
    --data '{
              "ref": "main",
              "inputs":{
                "input1":"some value",
                "input2":"some value 2"
              }
            }' \
    https://api.github.com/repos/n8ebel/GitHubActionsAutomationSandbox/actions/workflows/workflow_dispatch_example.yml/dispatches
```

- The `ref` input corresponds to the `branch`, `tag`, or `commit` you want the workflow to be run on.
- The `inputs` input corresponds with the inputs defined in the workflow file, and with what is present in the UI when triggering the workflow from GitHub

## Resources
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
- [GitHub Actions Documentation](https://docs.github.com/en/free-pro-team@latest/actions)
- [Git Hooks to Enforce Code Quality](https://proandroiddev.com/ooga-chaka-git-hooks-to-enforce-code-quality-11ce8d0d23cb)
- [Creating a Pull Request Template for Your Repository](https://help.github.com/en/articles/creating-a-pull-request-template-for-your-repository)
- [Closing GitHub Issues With Keywords](https://help.github.com/en/articles/closing-issues-using-keywords)
- [Danger Reference](https://danger.systems/ruby/)
- [Getting Started With Danger](https://danger.systems/guides/getting_started.html#including-danger)
- [Automating Code Review Tasks for Multi-Module Android Projects](https://blog.bitrise.io/automating-code-review-tasks-for-multi-module-android-projects)
- [Gradle Play Publisher Plugin](https://github.com/Triple-T/gradle-play-publisher)
- [Firebase App Distribution](https://firebase.google.com/products/app-distribution?utm_source=crashlytics_beta_marketing&utm_medium=redirect&utm_campaign=crashlytics_beta_redirect)
- [Danger Checkstyle Format](https://github.com/noboru-i/danger-checkstyle_format)
- [Gradle Versions Plugin](https://github.com/ben-manes/gradle-versions-plugin)

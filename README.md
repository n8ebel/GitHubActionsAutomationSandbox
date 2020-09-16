![Android CI](https://github.com/n8ebel/GitHubActionsAutomationSandbox/workflows/Android%20CI/badge.svg)
![Do Something That Needs Scheduled](https://github.com/n8ebel/GitHubActionsAutomationSandbox/workflows/Do%20Something%20That%20Needs%20Scheduled/badge.svg)

Example repo demonstrating different types of automated tasks and CI integrations

## Examples Included
- Simple GitHub Actions build configuration
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

## Triggering Workflows

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


## Resources
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

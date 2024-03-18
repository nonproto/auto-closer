# Auto Issue Closer

This action closes all issues that have a specific label  The changes from this vs upstream (https://github.com/lowply/auto-closer), is it doesn't default to 1.  So this action is good for labeling issues for a release.

## Environment variables

- `AC_LABEL` (_required_): The label that the target issue should have.
- `AC_KEEP` (_optional_): The number of the issues should be kept open. Default value: `0`

## Workflow example

```
name: weekly report
on:
  schedule:
  - cron: "0 0 * * 2"
jobs:
  close:
    needs: open
    name: Close old issues
    runs-on: ubuntu-latest
    steps:
    - uses: nonproto/auto-closer@v0.0.5
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        AC_LABEL: "report"
        AC_KEEP: 3
```

## Running locally for development

This is designed to be used as a GitHub Action, but you can also just build and run it locally with the following env vars:

```
cd src
export GITHUB_TOKEN="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
export GITHUB_REPOSITORY="owner/repository"
export AC_LABEL="label"
go run .
```

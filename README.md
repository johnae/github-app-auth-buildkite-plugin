# Github App Auth Buildkite Plugin

A [Buildkite plugin](https://buildkite.com/docs/agent/v3/plugins) that lets you
allows your pipeline to authenticate as a github app.

It requires that you provide a private key file, available to the agent in the
`GITHUB_APP_RSA_KEY_FILE` environment variable. This of course means that the
agent where you build runs should be secured as it can assume the identity of
the github app. Basically - only run trusted pipelines on the agent.

## Example

The required configuration is the installation_id and the app_id of the github app
you authenticate as. The generated token is valid for 10 minutes and is available in
the `GH_TOKEN` environment variable.

```yml
steps:
  - label: ":github: Open Github Issue"
    plugins:
      - johnae/github-app-auth#v1.0.1:
          installation_id: 123456
          app_id: 54321
    command: gh issue create --title "Example" --body "ignore me" --repo johnae/github-app-auth
```

Again, remember to provide the github app rsa key file to the agent in the environment variable
`GITHUB_APP_RSA_KEY_FILE` for this to work.

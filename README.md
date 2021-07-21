# GitHub Actions CI demo through REST API

This is a basic demonstration of what is needed to run a GitHub Actions CI build by calling their REST API.

We are using Figmagic for this demo to demonstrate running it in CI. Even if you don't care for that specific tool, you'll get the gist of how to automate stuff in CI.

## Example call to API

Set the following headers:

- `Accept`: `application/vnd.github.v3+json`
- `Content-Type`: `application/json`
- `Authorization`: `token {YOUR_PERSONAL_ACCESS_TOKEN}`

Then send a payload:

```json
POST https://api.github.com/repos/{USER_NAME}/{REPO_NAME}/actions/workflows/{WORKFLOW_FILENAME}/dispatches

{
	"ref": "main"
}
```

If you want to send in inputs, the format is:

```json
{
  "ref": "main",
  "inputs": {
    "message": "No message",
    "version": "latest"
  }
}
```

Only inputs that the workflow expects will be allowed. If it contains anything unexpected, the call will fail.

## References

- [GitHub Docs: Creating a personal access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)
- [GitHub Docs: Authentication in a workflow](https://docs.github.com/en/actions/reference/authentication-in-a-workflow)

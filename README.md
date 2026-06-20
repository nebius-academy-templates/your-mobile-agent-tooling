⌨️ In this practice task, you'll connect a PR review agent to GitHub through an MCP server and run an end-to-end review against a live pull request from the practice repository.

## 👩‍💻 Workflow at a glance

1. Set up your environment
2. Wire the GitHub MCP server
3. Verify the connection
4. Run against PR-01 (clean PR)
5. Test the publish gate
6. Capture your test session
7. Check your work
8. Submit

## 1. Set up your environment

1. Check that the repo `your-mobile-agent-tooling` appears in your GitHub account. 
2. Generate a GitHub personal access token with `pull_requests: read` and `contents: read` permissions for the practice repository.

## 2. Wire the GitHub MCP server

Set up the GitHub MCP server using your tool's configuration. Make sure your GitHub personal access token is set in the MCP server environment.

Ensure your MCP configuration file is listed in `.gitignore` before committing anything.

## 3. Verify the connection

Restart your tool and confirm the GitHub MCP tools are available. 

You should see `get_pull_request` and `create_review_comment` in the list of available tools.

If the GitHub tools do not appear:

- Confirm your MCP configuration file has valid JSON (no trailing commas, all quotes closed).
- Confirm the token has the correct scopes (see step 1).
- Restart your tool.

## 4. Run against PR-01

PR-01 in the practice repository is a clean pull request with no intentional issues. 

The practice repo is danielciolfi/mobile-pr-review-practice — you'll use it in this and the following lessons.

Ask the agent: 

```
Review PR #1 from danielciolfi/mobile-pr-review-practice
```

The agent should:

1. Call `get_pull_request` to fetch the diff
2. Apply the review criteria from your agent instructions file
3. Produce per-file output (no findings expected for a clean PR)
4. Pause and ask for confirmation before posting

## 5. Test the publish gate

When the agent asks whether to post, answer `no`. Confirm the agent does not post the comment.

### Tips

- If the agent posts without asking, the Guardrails section of your agent instructions file is missing or too vague. Add: "Always ask for confirmation before posting a comment to GitHub. Do not post unless the user responds with 'yes' or 'post'."
- For PR-01 (clean PR), the agent may report "No findings." The output structure (per-file sections and summary paragraph) should still appear.

## 6. Capture your test session

Copy the full conversation from your test session — the PR-01 review and the publish-gate test — or have your tool capture it. Save it as `test-session-2.md`.

This transcript is your evidence that the agent fetched live data and that the publish gate held, even with real write access available.

**Your transcript should show:**

- The agent calling `get_pull_request` and producing structured output for PR-01
- The agent asking for confirmation before posting
- The agent not posting after you answered `no`

## 7. Check your work

- [ ]  GitHub MCP server configured and connected
- [ ]  MCP configuration file is in `.gitignore`
- [ ]  GitHub tools (`get_pull_request`, `create_review_comment`) appear as available
- [ ]  The agent produced structured output for PR-01 (per-file sections and summary, no findings)
- [ ]  Publish gate held — agent asked for confirmation and did not post after you answered `no`
- [ ]  `test-session-2.md` shows evidence of the run and the publish-gate test

## 8. Submit your task

1. Commit your changes.
2. Push to GitHub.
3. Return to the lesson and click "Submit."

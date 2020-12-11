# Gitlab tools I use

## gitlab-logs

I often end up having to investigate an error that happened in the past;
this tools allows me to search for occurrences of an error using a regex
over the job logs.

To install it:

```sh
curl -LO https://raw.githubusercontent.com/maelvls/gitlab-tools/main/gitlab-logs
sudo install gitlab-logs /usr/local
sudo apt install curl jq perl
```

Example:

```sh
gitlab-logs --regex "UPGRADE FAILED" --env dev
```

More documentation is available in `--help`:

```
% gitlab-logs --help
Find logs that match a given regex. If no regular expression is given, all the
recent logs will be returned. When run in an existing gitlab clone, the server
and repository name will be picked up automatically.

Usage:
    gitlab-logs [options]

Options:
    --regex REGEX     Filter the logs with a simple grep regex.
                      Example: "UPGRADE FAILED".
    --env ENV         Only search through the logs of this environment.
                      Example: "dev".
    --status STATUS   Only search for jobs that have this status, can be one of
                      [created, running, success, failed, canceled]. Not enabled
                      by default.
    --token PAT       The personel access token (or oauth token) to be used to
                      authenticate requests to the Gitlab API. It is advised to
                      use the variable GITLAB_TOKEN instead of passing the token
                      as a CLI argument with --token.
    --server URL      The Gitlab instance you will be using; you can also use
                      the variable GITLAB_SERVER to do the same thing.
                      Default to https://gitlab.com, or the first remote's url
                      if you are in a git repo.
    --repo SLUG       The repo slug, i.e., username/repo_name. Can be set using
                      GITLAB_SLUG. If you are in a git repo that has a remote,
                      the first remote's url will be used by default.
    -d                Debug mode. Shows the 'curl' command when API calls are
                      made.

Environment variables:
    GITLAB_TOKEN      The token to use to access the GitLab API v4. To create a
                      token: https://gitlab.com/profile/personal_access_tokens
    GITLAB_SERVER     The Gitlab instance you will be using.
    GITLAB_SLUG       The repo slug.

Maël Valais, 2020
```

## gitlab-diff-jobs

```
% gitlab-diff-jobs --help
Does a diff of two artifacts paths given two job ids. The path is relative to
the root of the artifact archive.

Usage:
    gitlab-diff-jobs JOB_ID_LEFT JOB_ID_RIGHT ARTIFACT_PATH [options]

Options:
    --token PAT       The personel access token (or oauth token) to be used to
                      authenticate requests to the Gitlab API. It is advised to
                      use the variable GITLAB_TOKEN instead of passing the token
                      as a CLI argument with --token.
    --server URL      The Gitlab instance you will be using; you can also use
                      the variable GITLAB_SERVER to do the same thing.
                      Default to https://gitlab.com, or the first remote's url
                      if you are in a git repo.
    --repo SLUG       The repo slug, i.e., username/repo_name. Can be set using
                      GITLAB_SLUG. If you are in a git repo that has a remote,
                      the first remote's url will be used by default.
    -d                Debug mode. Shows the 'curl' command when API calls are
                      made.
    --difftool        The tool to used to display the diff. Default to
                      "code --diff".
    --preprocess      Run a command on both files before passing it to the diff
                      tool. Example: you can remove trailing whitespaces
                      with --preprocess "sed 's/ *$//'". The command given with
                      --preprocess is given the file on stdin and must output on
                      stdout.

Maël Valais, 2020
```
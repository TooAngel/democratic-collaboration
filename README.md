# world driven

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/a3385a0433a649be95639b8a59fcb6fe)](https://www.codacy.com/app/TooAngel/worlddriven?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=TooAngel/worlddriven&amp;utm_campaign=Badge_Grade)
[![CircleCI](https://circleci.com/gh/TooAngel/worlddriven.svg?style=svg)](https://circleci.com/gh/TooAngel/worlddriven)
[![gitter](https://badges.gitter.im/worlddriven/Lobby.svg)](https://gitter.im/worlddriven/Lobby)
[![Code climate](https://api.codeclimate.com/v1/badges/ec4136b6d2eeff72f192/maintainability)](https://codeclimate.com/github/TooAngel/worlddriven/maintainability)

Hosted under https://www.worlddriven.org

World driven introduces a contribution based weighted voting system
for merging of pull requests. As soon as you contribute to a project, you get a share or
responsibility for the progress of the project.


Github Pull Request are the main contact point. Reviewing a PR with an
'Approve' votes for `yes`, 'Request change' is `no`.

The number of commits on the repository is the weight for the vote.

If a PR is ready for merge a voting is started (starting `value` 0):
 - If a reviewer 'Request changes' the `value` decreases by their contribution value.
 - If a reviewer 'Approve' the `value` increases by their contribution value.
 - Based on the `value` and `total` of votes is `coefficient` is calculated and
   the PR is merged in `coefficient * (5 + pull_request.commits * 5)) days`.

## Vision

Having clear and automated rules for progressing in open source projects is just the base. Due to the DevOps (or GitOps) idea many operational tasks are now stored in repositories, too, and applied on merge. So the challenge is building (worlddriven) services, which are only maintained via Pull Requests. This provides a new level of trust and a new entity unavailable system data (still searching for a better name). Passwords, service credentials, ... is data which does not necessarily be accesible by humans. This can be maintained and used only in the system.

Example: In one of the company I was working for the employees were using chromeboxes. Within their daily work they had to split and merge PDFs. There are a lot of (free) services out there which just do the job, but they can't be used. What happens with my PDFs, do they store them, do they use them. I hope and guess not, but I'm not sure.

How about a PDF service, open source, world driven, continous deployment. No one has access to any credentials, changes can only be done via public Pull Requests. That should be fine?

## How it Works

    - A Pull Request gets automatic merged after some time.
    - Contributors of the project can vote by reviewing the Pull Request.
    - Votes are weighted based on the number of commits on the repository. The according share is added or subtracted from the time to merge.
    - If it exceeds the default time, more votes against the merge, the merge is not executed.

This way a review can speed up the merge process. Or can prolong or stop it to discuss the concerns.

A status check is used to inform about the time to merge and provides a link for a detailed breakdown.

## Why?
    - Due to the clear rules it is easy to see what happens with your PR and when it will be merged.
    - Some open source projects struggle with their maintainer. This way others can still drive the project forward.
    - Weighting the votes enables the main contributors the most power to stale or block bad PRs or speed things up. On the other hand it can motivate to contribute to increase their own weight.
    - One fundamental question is the ownership. Currently the owner of the project has anyway full control and can stop or speed up everything. It would be nice if they don't have to.

I'm pretty sure the system can be tricked with certain behavior, that's not the idea. Working on an open source project is collaborating, so most of the tricking can easily solved by communication.

## Current Rules
    - 10 days, well more then a week, should give everyone enough time to look into
    - per commit: If a PR has multiple commits the time is increased for each commit. Having multiple commits on a - PR means the feature reaches a certain complexity, hence reviewers should have enough time to review it.
    - Voting via review: Github reviewing functionality is the perfect place to discuss the PR and express the preference. (Gitlab the same, but not yet implemented)

## Develop

Run `python src/server.py`.
For github oauth feature provide `GITHUB_CLIENT_ID` and `GITHUB_CLIENT_SECRET`,
callback url is `/github-callback`.
Set Session secret as `SESSION_SECRET` initial a random string.

Run tests with: `pytest`

## Api

- `/v1/:org/:repo/` e.g. `/v1/tooangel/worlddriven/`
  to get info about the repository

  Response:
```
{
    "archive_url": "https://api.github.com/repos/TooAngel/worlddriven/{archive_format}{/ref}",
    "assignees_url": "https://api.github.com/repos/TooAngel/worlddriven/assignees{/user}",
    "blobs_url": "https://api.github.com/repos/TooAngel/worlddriven/git/blobs{/sha}",
    "branches_url": "https://api.github.com/repos/TooAngel/worlddriven/branches{/branch}",
    "clone_url": "https://github.com/TooAngel/worlddriven.git",
    "collaborators_url": "https://api.github.com/repos/TooAngel/worlddriven/collaborators{/collaborator}",
    "comments_url": "https://api.github.com/repos/TooAngel/worlddriven/comments{/number}",
    "commits_url": "https://api.github.com/repos/TooAngel/worlddriven/commits{/sha}",
    "compare_url": "https://api.github.com/repos/TooAngel/worlddriven/compare/{base}...{head}",
    "contents_url": "https://api.github.com/repos/TooAngel/worlddriven/contents/{+path}",
    "contributors_url": "https://api.github.com/repos/TooAngel/worlddriven/contributors",
    "created_at": "2017-01-11T08:59:45Z",
    "default_branch": "master",
    "deployments_url": "https://api.github.com/repos/TooAngel/worlddriven/deployments",
    "description": "Reviewer based weighted automatic pull request merging",
    "downloads_url": "https://api.github.com/repos/TooAngel/worlddriven/downloads",
    "events_url": "https://api.github.com/repos/TooAngel/worlddriven/events",
    "fork": false,
    "forks": 5,
    "forks_count": 5,
    "forks_url": "https://api.github.com/repos/TooAngel/worlddriven/forks",
    "full_name": "TooAngel/worlddriven",
    "git_commits_url": "https://api.github.com/repos/TooAngel/worlddriven/git/commits{/sha}",
    "git_refs_url": "https://api.github.com/repos/TooAngel/worlddriven/git/refs{/sha}",
    "git_tags_url": "https://api.github.com/repos/TooAngel/worlddriven/git/tags{/sha}",
    "git_url": "git://github.com/TooAngel/worlddriven.git",
    "has_downloads": true,
    "has_issues": true,
    "has_pages": true,
    "has_projects": true,
    "has_wiki": false,
    "homepage": "",
    "hooks_url": "https://api.github.com/repos/TooAngel/worlddriven/hooks",
    "html_url": "https://github.com/TooAngel/worlddriven",
    "id": 78621052,
    "issue_comment_url": "https://api.github.com/repos/TooAngel/worlddriven/issues/comments{/number}",
    "issue_events_url": "https://api.github.com/repos/TooAngel/worlddriven/issues/events{/number}",
    "issues_url": "https://api.github.com/repos/TooAngel/worlddriven/issues{/number}",
    "keys_url": "https://api.github.com/repos/TooAngel/worlddriven/keys{/key_id}",
    "labels_url": "https://api.github.com/repos/TooAngel/worlddriven/labels{/name}",
    "language": "Python",
    "languages_url": "https://api.github.com/repos/TooAngel/worlddriven/languages",
    "merges_url": "https://api.github.com/repos/TooAngel/worlddriven/merges",
    "milestones_url": "https://api.github.com/repos/TooAngel/worlddriven/milestones{/number}",
    "mirror_url": null,
    "name": "worlddriven",
    "network_count": 5,
    "notifications_url": "https://api.github.com/repos/TooAngel/worlddriven/notifications{?since,all,participating}",
    "open_issues": 5,
    "open_issues_count": 5,
    "owner": {
        "avatar_url": "https://avatars5.githubusercontent.com/u/131156?v=4",
        "events_url": "https://api.github.com/users/TooAngel/events{/privacy}",
        "followers_url": "https://api.github.com/users/TooAngel/followers",
        "following_url": "https://api.github.com/users/TooAngel/following{/other_user}",
        "gists_url": "https://api.github.com/users/TooAngel/gists{/gist_id}",
        "gravatar_id": "",
        "html_url": "https://github.com/TooAngel",
        "id": 131156,
        "login": "TooAngel",
        "organizations_url": "https://api.github.com/users/TooAngel/orgs",
        "received_events_url": "https://api.github.com/users/TooAngel/received_events",
        "repos_url": "https://api.github.com/users/TooAngel/repos",
        "site_admin": false,
        "starred_url": "https://api.github.com/users/TooAngel/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/TooAngel/subscriptions",
        "type": "User",
        "url": "https://api.github.com/users/TooAngel"
    },
    "permissions": {
        "admin": true,
        "pull": true,
        "push": true
    },
    "private": false,
    "pulls_url": "https://api.github.com/repos/TooAngel/worlddriven/pulls{/number}",
    "pushed_at": "2017-07-15T20:13:36Z",
    "releases_url": "https://api.github.com/repos/TooAngel/worlddriven/releases{/id}",
    "size": 154,
    "ssh_url": "git@github.com:TooAngel/worlddriven.git",
    "stargazers_count": 10,
    "stargazers_url": "https://api.github.com/repos/TooAngel/worlddriven/stargazers",
    "statuses_url": "https://api.github.com/repos/TooAngel/worlddriven/statuses/{sha}",
    "subscribers_count": 1,
    "subscribers_url": "https://api.github.com/repos/TooAngel/worlddriven/subscribers",
    "subscription_url": "https://api.github.com/repos/TooAngel/worlddriven/subscription",
    "svn_url": "https://github.com/TooAngel/worlddriven",
    "tags_url": "https://api.github.com/repos/TooAngel/worlddriven/tags",
    "teams_url": "https://api.github.com/repos/TooAngel/worlddriven/teams",
    "trees_url": "https://api.github.com/repos/TooAngel/worlddriven/git/trees{/sha}",
    "updated_at": "2017-07-15T13:15:53Z",
    "url": "https://api.github.com/repos/TooAngel/worlddriven",
    "watchers": 10,
    "watchers_count": 10
}
```

 - `/v1/:org/:repo/pull/:number` e.g. `/v1/tooangel/worlddriven/pull/43/`
   to get info about the pull request

   Response:
```
{
    "coefficient": 0.9764705882352941,
    "contributors": {
        "TooAngel": 80,
        "WhiteHalmos": 1,
        "cbek": 1,
        "codacy-badger": 1,
        "pst": 2
    },
    "mergeable": true,
    "pull_request": {
        "number": 43,
        "title": "Add Angular UI",
        "url": "https://api.github.com/repos/TooAngel/worlddriven/pulls/43",
        "user": {
            "avatar_url": "https://avatars6.githubusercontent.com/u/253456?v=4",
            "bio": null,
            "blog": "https://coreos.com",
            "company": "@coreos",
            "created_at": "2010-04-26T20:24:24Z",
            "email": null,
            "events_url": "https://api.github.com/users/pst/events{/privacy}",
            "followers": 8,
            "followers_url": "https://api.github.com/users/pst/followers",
            "following": 0,
            "following_url": "https://api.github.com/users/pst/following{/other_user}",
            "gists_url": "https://api.github.com/users/pst/gists{/gist_id}",
            "gravatar_id": "",
            "hireable": null,
            "html_url": "https://github.com/pst",
            "id": 253456,
            "location": "Berlin, Germany",
            "login": "pst",
            "name": "Philipp Strube",
            "organizations_url": "https://api.github.com/users/pst/orgs",
            "public_gists": 2,
            "public_repos": 23,
            "received_events_url": "https://api.github.com/users/pst/received_events",
            "repos_url": "https://api.github.com/users/pst/repos",
            "site_admin": false,
            "starred_url": "https://api.github.com/users/pst/starred{/owner}{/repo}",
            "subscriptions_url": "https://api.github.com/users/pst/subscriptions",
            "type": "User",
            "updated_at": "2017-07-14T16:47:15Z",
            "url": "https://api.github.com/users/pst"
        }
    },
    "reviews": {
        "TooAngel": {
            "date": "2017-07-15T14:51:10Z",
            "value": 1
        },
        "cbek": {
            "date": "2017-07-15T14:54:30Z",
            "value": 1
        }
    },
    "votes": 83,
    "votes_total": 85
}
```

## Production environment

Started on some random server in `screen`, with
`while true; do bash run.sh; done`

Get `GET /restart/` stops the server process and restarted by the command
line command. Super ugly I know, just quickly solved somehow.

## Links

- https://www.w3schools.com/howto/howto_css_switch.asp

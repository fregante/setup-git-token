## ⚠️ Deprecated

Starting with the v2 of [actions/checkout](https://github.com/actions/checkout), the token will be automatically set **however** you'll still have to manually set the commit author and email. It's best you use the new [fregante/setup-git-user](https://github.com/fregante/setup-git-user) action instead:

### Old version: `actions/checkout@v1` + `setup-git-token`

```yml
    - uses: actions/checkout@v1
    - uses: fregante/setup-git-token@v1
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
```

### New version: `actions/checkout@v2` + [`setup-git-user`](https://github.com/fregante/setup-git-user)

```yml
    - uses: actions/checkout@v2
    - uses: fregante/setup-git-user@v1
```

### Verbose action-less version

You don't really need an action anymore, but it's slightly more verbose:

```yml
    - uses: actions/checkout@v2
    - run: git config user.name "GitHub Actions"
    - run: git config user.email "actions@users.noreply.github.com"
```

---

# setup-git-token

This action sets the `GITHUB_TOKEN` as credentials for git, allowing `git push` in successive steps. Additionally, the committer's `email` and `name` are also set.

# Usage

See [action.yml](action.yml)

Basic:

```yaml
    steps:
    - uses: actions/checkout@master
    - uses: fregante/setup-git-token@v1
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
    - run: git branch new-branch
    - run: git push origin new-branch
```

By default, new commits and tags will be assigned to the [@actions](https://github.com/actions) user. If you wish to customize the committer, specify that using `with.email` and `with.name`:

```yaml
    - uses: fregante/setup-git-token@v1
      with:
        name: The Bot
        email: bot@example.com
```

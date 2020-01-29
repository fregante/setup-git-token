## (No longer necessary)

GitHub's own [`actions/checkout`](https://github.com/actions/checkout) at version 2 will automatically set up your token, **however** unlike with `setup-git-token` you'll have to manually set the commit author and email, so you might want to continue using this action for that reason.

### With setup-git-token

```yml
    - uses: actions/checkout@v2
    - uses: fregante/setup-git-token@v1
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
```

### Without setup-git-token

```yml
    - uses: actions/checkout@v2
    - run: git config user.name "GitHub Actions" && git config user.email "actions@users.noreply.github.com"
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

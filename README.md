## Auto bump cpanfile

> The example repository for auto bump to `cpanfile` and `cpanfile.snapshot`

### The contain files

```
.github/workflows/
  composite/
    update-cpan-module/action.yml - The update action for CPAN mdoule.
  workflows/
    bump-cpanfile-manually.yml - Updating CPAN module manually.
    bump-cpanfile-schedule.yml - Updating CPAN module by scheduled cron.
    chatops-cpanfile.yml - The file for ChatOps on pull request issue comments.
```

#### `composite/update-cpan-module/action.yml`

This file is a composite action for bump single CPAN modules.

The `inputs` arguments as follows:

- `perl-version` - the runtime version of perl
- `module` - the module name to updating target
- `cpanfile` - the path to `cpanfile`
- `branch-prefix` - the branch name prefix of bump pull request
- `commit-message` - the template string for commit message
- `pull-request-title` - the template string for pull request title
- `pull-request-body` - the template string for pull request comment body

The `commit-message`, `pull-request-title` and `pull-request-body` can be use `@varname@` template variables,
it supports to as follows:

- `@module@` - The CPAN module name
- `@version@` - The CPAN mdoule version
- `@dist@` - The distribution name of CPAN module

#### `workflows/bump-cpanfile-manually.yml`

This file is for the updating single CPAN module by manually action.

The arguments of this action as follows:

- `env.perl-version` - the runtime version of perl
- `inputs.module` - the CPAN module name for updating

#### `workflows/bump-cpanfile-schedule.yml`

This file is for the updating `cpanfile` by scheduled times, or manually.

The arguments of this action as follows:

- `env.perl-version` - the runtime version of perl
- `env.cpanfile` - the path to `cpanfile`

#### `workflows/chatops-cpanfile.yml`

This file is for the chatops by issue comment on the bump pull request.

The arguments as follows:

- `env.perl-version` - the runtime version of perl
- `env,commit-message-prefix` - the prefix string for grep bump commit from pull request
- `env.commit-message-regexp` - the regexp for extracing the CPAN module name

The format of `commit-message-regexp` is `s///` code on perl,
please looking to this file, about how to used that setting.

The chatops command as follows:

- `/recreate`
  - recreate the pull request
  - this command useful for fix conflict `cpanfile.snapshot`

### Author

OKAMURA Naoki aka nyarla / kalaclista <nyarla@kalaclista.com>

### License

[ISC](./LICENSE.md)

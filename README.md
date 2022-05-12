# commits-author-name

This is a simple repo that serve as a tutorial to change Author's Name for Github commits.

## From now onwards

To change the authors name from now onwards you can do it globally or just in a single repo.

- Globally:
```bash
git config --global user.name "John Doe"
git config --global user.email "john@doe.org"
```

- Single repo:
```bash
git config user.name "John Doe"
git config user.email "john@doe.org"
```

## Past commits

You would need to execute the following command:

NOTICE: Change values for 'WRONG_EMAIL', 'NEW_NAME' and 'NEW_EMAIL'.

```bash
git filter-branch --env-filter '
WRONG_EMAIL="wrong@example.com"
NEW_NAME="New Name Value"
NEW_EMAIL="correct@example.com"

if [ "$GIT_COMMITTER_EMAIL" = "$WRONG_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$NEW_NAME"
    export GIT_COMMITTER_EMAIL="$NEW_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$WRONG_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$NEW_NAME"
    export GIT_AUTHOR_EMAIL="$NEW_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
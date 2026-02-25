The new alias:
`up = "!f() { git pull --autostash --rebase --prune origin $(git rev-parse --abbrev-ref HEAD) \"$@\" && git submodule update --init --recursive; }; f"`

1.  **`!f() { ... }; f`**: This is a standard git alias pattern to define and execute a shell function. It allows for complex logic like variables and multiple commands.
2.  **`git rev-parse --abbrev-ref HEAD`**: This command dynamically gets the name of your current branch (e.g., `feat/image-set-use-case`).
3.  **`origin $(...)`**: By explicitly passing the remote (`origin`) and the branch name, we bypass the need for git to have "tracking" information set. It will always try to pull the current branch name from origin.
4.  **`"$@"`**: This forwarding syntax ensures that any additional arguments you pass to the alias (like `git up --no-rebase`) are correctly handed off to the `git pull` command.
5.  **`&& git submodule update...`**: The `&&` ensures that submodules are only updated if the pull command succeeds.

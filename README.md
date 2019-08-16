# Purpose
While using the excellent [proselint](https://github.com/amperser/proselint) through [flycheck](https://github.com/flycheck/flycheck), I noticed that it would list annotations such as TODO with a warning. This served as a handy list of issues to address within a writing project. Another annotation that I like to use is `CITE`, to remind myself to find a citation. This was not flagged by proselint, so I decided that a simple regex could catch both and I'd pass it through to flycheck to get a handy list.

# Installation
1. Install [ripgrep](https://github.com/BurntSushi/ripgrep) (available in most distributions' package repositories). The shell script can be easily modified to use e.g. GNU grep.
2. Place the `todo-checker` file somewhere in your `PATH`, and make sure that it has executable permissions.
3. Add the following to your `.emacs` (not tested, but should work) or `dotspacemacs/user-config` in your `.spacemacs` file. Add modes other than `markdown-mode` if you'd like.
```elisp
  (flycheck-define-checker todo-checker
    "A checker to list open TODOs, CITEs, or other annotations in
  a file."
    :command ("todo-checker" source)
    :error-patterns
    ((warning line-start (file-name) ":" line ":" column ":" (message) line-end))
    :modes markdown-mode))
```
4. When in `markdown-mode`, change the checker to `todo-checker`. In Spacemacs, this is `SPC e s todo-checker RET`.
5. Open the list of TODOs and CITEs using the flycheck error list. In Spacemacs, this is `SPC e l`.
6. Profit.

# microsoft-word

Testing Word changes tracking via Git.

According to <https://blog.front-matter.io/posts/using-microsoft-word-with-git/>, it is possible to track changes in Microsoft Word documents via Git.
This repository tests how well it works.

To do so, `.gitattributes` contains:

```
*.docx diff=pandoc2markdown
```

and the following was added to `.git/config`:

```
[diff "pandoc2markdown"]
    textconv="pandoc --to=markdown"
    prompt=false
```

## Conclusion

Git does show the correct diff when running `git diff` locally.
It shows the Markdown changes.
GitHub, however, just shows the `text.docx` changes as changes to a binary.
This makes sense because `.git/config` is ignored by GitHub and GitHub cannot run arbitrary binaries during the diff.
There is a proposal for Gitea to support this: https://github.com/go-gitea/gitea/issues/12288.

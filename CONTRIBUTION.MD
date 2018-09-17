# **Contributing to Merge Request Inc. Projects**
____
## **Found an Issue?**
____
If you find a bug in the source code or a mistake in the documentation, you can help us by
submitting an issue to ours github repositories.
Each issue should be tagged with at least :

- an "issue type and priority" tag, either "tech-debt" for technical debt issues, or one of improvement, defect or critical for bugs.

Even better you can submit a Merge Request with a fix.

## **Submitting a Merge Request**
____
Before you submit your merge request consider the following guidelines:

* Search for an open or closed Merge Request
  that relates to your submission. You don't want to duplicate effort.
* Make your changes in a new git branch:

    ```shell
    git checkout -b my-fix-branch master
    ```

* Create your patch, **including appropriate test cases**.
* Run the full project test suite,
  and ensure that all tests pass.
* Commit your changes using a descriptive commit message that follows our
  [commit message conventions](#git-commit-guideline). Adherence to the [commit message conventions](#git-commit-guideline) is required,
  because release notes are automatically generated from these messages.

    ```shell
    git commit -a
    ```
  Note: the optional commit `-a` command line option will automatically "add" and "rm" edited files.

* Push your branch to Github:

    ```shell
    git push origin my-fix-branch
    ```

In Github, send a merge request to `master`.
If we suggest changes, then:

* Make the required updates.
* Re-run the full test suite to ensure tests are still passing.
* Commit your changes to your branch (e.g. `my-fix-branch`).
* Push the changes to your Github repository (this will update your Pull Request).

If the PR gets too outdated we may ask you to rebase and force push to update the PR:

```shell
git rebase master -i
git push origin my-fix-branch -f
```

_WARNING: Squashing or reverting commits and force-pushing thereafter may remove Github comments
on code that were previously made by you or others in your commits. Avoid any form of rebasing
unless necessary._

#### After your merge request is merged

After your merge request is merged, you can safely delete your branch and pull the changes
from the main (upstream) repository:

* Delete the remote branch on Github either through the Github web UI or your local shell as follows:

    ```shell
    git push origin --delete my-fix-branch
    ```

* Check out the master branch:

    ```shell
    git checkout master -f
    ```

* Delete the local branch:

    ```shell
    git branch -D my-fix-branch
    ```

* Update your master with the latest upstream version:

    ```shell
    git pull --ff upstream master
    ```

## **Git Commit Guideline**
____
We have very precise rules over how your git commit messages can be formatted.  This leads to **more
readable messages** that are easy to follow when looking through the **project history**.
But also, we use the git commit messages to **generate releases changelogs**.

### Commit Message Format
Each commit message consists of a **header**, a **body** and a **footer**.  The header has a special
format that includes a **type**, a **scope** and a **subject**:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

The **header** is mandatory and the **scope** of the header is optional.

Any line of the commit message cannot be longer 100 characters! This allows the message to be easier
to read in various git tools.

### Type
Must be one of the following:

* **feat**: A new feature
* **fix**: A bug fix
* **docs**: Documentation only changes
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing
  semi-colons, etc)
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **perf**: A code change that improves performance
* **test**: Adding missing or correcting existing tests
* **chore**: Changes to the build process or auxiliary tools and libraries such as documentation
  generation
* **other**: Anything else that do not really matter

### Scope
The scope could be anything specifying place of the commit change.<br />
For example `api`, `entities`, etc...

You can remove the scope when the change affects more than a single scope.<br />
Ex : `chore: Bump to next snapshot iteration`

### Subject
The subject contains succinct description of the change:

* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize first letter
* no dot (.) at the end

### Body
Just as in the **subject**, use the imperative, present tense: "change" not "changed" nor "changes".
The body should include the motivation for the change and contrast this with previous behavior.

### Footer
The footer should contain any information about **Breaking Changes**

**Breaking Changes** should start with the word `BREAKING CHANGE:` with a space or two newlines.
The rest of the commit message is then used for this.

## **Version changes**
____
Version changes are splitted into 2 cases : [Release](#release-process) and [Patch](#patch-process)

### Release Process

The default release process consists of the following tasks:

 1. Check that the working directory is a git repository and the repository has no outstanding changes.
 1. If there are any snapshot dependencies, verify/fix their version.
 1. Remove the `-SNAPSHOT` from version (eg. `1.8.0-SNAPSHOT` to `1.8.0`).
 1. Generate your changelog
 1. Commit the version changes.
 1. Tag the previous commit with `v$major.$minor.$patch` (eg. `v1.8.0`).
 1. Run the full test suite, if any test fails, the release process is aborted.
 1. Create a new branch based with `r$major.$minor` (eg. `r1.8`).
 1. Publish the release artifact.
 1. Bump to next snapshot version (eg. `1.8.0` to `1.9.0-SNAPSHOT`) on master.
 1. Bump to next snapshot patch version (eg. `1.8.0` to `1.8.1-SNAPSHOT`) on release branch.
 1. Commit the version changes.

In case of a failure of any of these task, the release process is aborted.

### Patch Process

The default patch process consists of the following tasks:

 1. Check that the working directory is a git repository and the repository has no outstanding changes.
 1. Check that your work is based on the correct branch name (eg. `r1.8`)
 1. **Do not** create a new branch in case of a patch, just use the release based branch
 1. If there are any snapshot dependencies, verify/fix their version.
 1. Remove the `-SNAPSHOT` from version (eg. `1.8.3-SNAPSHOT` to `1.8.3`).
 1. Generate your changelog
 1. Commit the version changes.
 1. Tag the previous commit with `v$major.$minor.$patch` (eg. `v1.8.3`).
 1. Run the full test suite, if any test fails, the patch process is aborted.
 1. Publish the release artifact.
 1. Bump to next snapshot version (eg. `1.8.3` to `1.8.4-SNAPSHOT`).
 1. Commit the version changes.

In case of a failure of any of these task, the patch process is aborted.


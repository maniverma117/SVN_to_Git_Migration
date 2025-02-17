# SVN to Git Migration

```markdown
This guide provides detailed instructions for migrating an SVN repository to Git using Docker and `git svn`. It covers the following steps:

1. Running Docker Container for SVN to Git Migration
2. Setting Up SVN Repository
3. Loading Data into SVN Repository
4. Cloning SVN Repository into Git 
5. Viewing Git Commit History

## 1. Run Docker Container for SVN to Git Migration

The migration process starts by running a Docker container that includes all necessary tools for SVN to Git migration. This container runs an interactive bash shell.

docker run -itd maniverma/svn-to-git-migrator:v1 bash
```

This command pulls the Docker image `maniverma/svn-to-git-migrator:v1` (if not already pulled) and starts it with an interactive shell (`bash`).

## 2. Set Up SVN Repository

The next step is to create a new SVN repository using `svnadmin`.

### Create SVN Repository:

```bash
svnadmin create /var/opt/svn/myrepo
```

This will create a new SVN repository at `/var/opt/svn/myrepo`. You can change the path as needed.

### Load Data into SVN Repository:

To load data from a dump file (e.g., `Test_repo_07-02-2025.dump`) into the newly created SVN repository:

```bash
svnadmin load /var/opt/svn/myrepo < VisualSVN/Test_repo_07-02-2025.dump
```

This will import the SVN dump file into the repository.

## 3. Verify SVN Repository

After setting up the SVN repository, you can verify its contents and history with the following commands.

### Check SVN Log:

```bash
svn log file:///VisualSVN/myrepo/
```

This will display the commit history of the SVN repository.

### Check SVN Info:

```bash
svn info file:///VisualSVN/myrepo/
```

This shows information about the repository, such as the repository URL, UUID, and the latest revision.

### List Contents of the SVN Repository:

```bash
svn list file:///VisualSVN/myrepo/
```

This lists the top-level contents of the SVN repository.

### List Contents of `Test_repo` Directory:

```bash
svn list file:///VisualSVN/myrepo/Test_repo/
```

This lists the contents of the `Test_repo` directory within the SVN repository.

## 4. Clone SVN Repository into Git

Now you can convert the SVN repository into a Git repository. Since the repository structure follows a standard layout (`trunk/`, `branches/`, `tags/`), you can use the `--stdlayout` flag.

### Clone SVN Repository into Git:

```bash
git svn clone --stdlayout file:///VisualSVN/myrepo/Test_repo/ --no-metadata my_git_repo
```

This command will clone the SVN repository into a Git repository called `my_git_repo`. The `--no-metadata` flag prevents the creation of Git metadata in the SVN commits.

## 5. View Git Commit History

After cloning the repository, navigate into the new Git repository and check the commit history.

### Navigate to Git Repository:

```bash
cd my_git_repo/
```

### List Files in the Git Repository:

```bash
ls
```

### View Git Commit History:

To view the commit history in a clean and graphical format, run:

```bash
git log --graph --oneline --decorate --all
```

This command displays the commit history in a graphical format, showing commit hashes (`--oneline`), decorated with branch and tag names (`--decorate`), and all commits from all branches (`--all`).

---

## Summary

This migration process allows you to easily convert an SVN repository to Git using Docker, `svnadmin`, and `git svn`. By following these steps, you can efficiently migrate your project from SVN to Git while preserving the commit history.
```

### Key Points:
1. Docker: Runs a container that includes necessary tools.
2. SVN Setup: Creates and loads data into an SVN repository using `svnadmin`.
3. SVN Verification: Commands to check the repository's info, history, and contents.
4. Git Cloning: Uses `git svn clone` to convert the SVN repository into a Git repository.
5. Git Log: Displays the commit history in a graphical format.


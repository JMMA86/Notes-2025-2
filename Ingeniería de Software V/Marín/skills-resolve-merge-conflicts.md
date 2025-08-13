## Step 1
### ⌨️ Activity: Create a pull request
1. Open a new browser tab, and work on the steps in your second tab while you read the instructions in this tab.
2. We made a small change to a file in the repository in the `my-resume` branch.
3. [Create a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) setting `my-resume` as the head branch and `main` as the base branch. You can enter `Resolving merge conflicts` for the pull request title and body.

![[Pasted image 20250811093345.png]]

4. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

## Step 2
### ⌨️ Activity: Resolve a merge conflict
1. Open the pull request that you just created, we created a conflict for you. Have no fear!
2. At the bottom of the page, under "This branch has conflicts that must be resolved", click the **Resolve conflicts** button.
3. Look for the highlighted sections that begins with `<<<<<<< my-resume` and ends with `>>>>>>> main`. These markers are added by Git to show you the content that is in conflict.
4. Remove the changes made on the main branch by deleting all of the content below the `=======` and above `>>>>>>> main`.
5. Next, remove the merge conflict markers by deleting the following lines:
    
    ```
    <<<<<<< my-resume
    =======
    >>>>>>> main
    ```
    
6. With the merge conflict markers removed, click **Mark as resolved**.

![[Pasted image 20250811093615.png]]

7. Finally, click **Commit merge**.
8. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

## Step 3
### ⌨️ Activity: Create your own conflict
We went ahead and added a new file called `references.md` and pushed that change to `main`, without updating your `my-resume` branch.

1. Browse to the `my-resume` branch.
2. Click the `Add file` dropdown menu and then on `Create new file`.
3. Create a file named `references.md`.
4. Enter some text that conflicts with what we added for `references.md` in the `main` branch.
5. Scroll to the bottom of the page and enter a commit message for your change.
6. Click the **Commit new file** button, making sure the "Commit directly to the `my-resume` branch" option is selected.

![[Pasted image 20250811093931.png]]

7. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

## Step 4
### ⌨️ Activity: Merge your pull request
1. First, resolve any remaining conflicts in your pull request.
    
    > Look back at step one if you need help.
    
2. Click **Merge pull request**.
3. Delete the branch `my-resume` (optional).

![[Pasted image 20250811094133.png]]

4. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

Course ended: [JMMA86/skills-resolve-merge-conflicts: My clone repository](https://github.com/JMMA86/skills-resolve-merge-conflicts)
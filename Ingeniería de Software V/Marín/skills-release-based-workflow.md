## Step 1
### ⌨️ Activity: Create a release for the current codebase
In this step, you will create a release for this repository on GitHub.

GitHub Releases point to a specific commit. Releases can include release notes in Markdown files, and attached binaries.

Before using a release based workflow for a larger release, let's create a tag and a release.

1. Open a new browser tab, and work on the steps in your second tab while you read the instructions in this tab.

![[Pasted image 20250811082701.png]]

2. Go to the **Releases** page for this repository.
    - _Tip: To reach this page, click the **Code** tab at the top of your repository. Then, find the navigation bar below the repository description, and click the **Releases** heading link._

![[Pasted image 20250811082739.png]]

3. Click **Create a new release**.

![[Pasted image 20250811082753.png]]

4. In the field for _Tag version_, specify a number. In this case, use **v0.9**. Keep the _Target_ as **main**.

![[Pasted image 20250811082822.png]]

5. Give the release a title, like "First beta release". If you'd like, you could also give the release a short description.

![[Pasted image 20250811082905.png]]

6. Select the checkbox next to **Set as a pre-release**, since it is representing a beta version.

![[Pasted image 20250811082931.png]]

7. Click **Publish release**.

![[Pasted image 20250811082948.png]]

### ⌨️ Activity: Introduce a bug to be fixed later

To set the stage for later, let's also add a bug that we'll fix as part of the release workflow in later steps. We've already created a `update-text-colors` branch for you so let's create and merge a pull request with this branch.

1. Open a **new pull request** with `base: release-v1.0` and `compare: update-text-colors`.

![[Pasted image 20250811083123.png]]

2. Set the pull request title to "Updated game text style". You can include a detailed pull request body, an example is below:

    ```
    ## Description:
    - Updated game text color to green
    ```

![[Pasted image 20250811083222.png]]

3. Click **Create pull request**.

![[Pasted image 20250811083245.png]]

4. We'll merge this pull request now. Click **Merge pull request** and delete your branch.

![[Pasted image 20250811083320.png]]
![[Pasted image 20250811083332.png]]

5. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

## Step 2
### ⌨️ Activity: Update `base.css`
1. Create a new branch off of the `main` branch and change the `body` CSS declaration in `base.css` to match what is below. This will set the page background to black.

```
body {
    background-color: black;
}
```

![[Pasted image 20250811084156.png]]

![[Pasted image 20250811084311.png]]

2. Open a pull request with `release-v1.0` as the `base` branch, and your new branch as the `compare` branch.

![[Pasted image 20250811084400.png]]

3. Fill in the pull request template to describe your changes.

![[Pasted image 20250811084441.png]]

4. Click **Create pull request**.

### ⌨️ Activity: Merge the pull request
1. Click **Merge pull request**, and delete your branch.

![[Pasted image 20250811084547.png]]

2. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

## Step 3
### ⌨️ Activity: Open a release pull request
Let's make a new pull request comparing the `release-v1.0` branch to the `main` branch.

1. Open a **new pull request** with `base: main` and `compare: release-v1.0`.
2. Ensure the title of your pull request is "Release v1.0".
3. Include a detailed pull request body, an example is below:
    
    ```
    ## Description:
    - Changed page background color to black.
    - Changed game text color to green.
    ```

![[Pasted image 20250811084835.png]]

4. Click **Create pull request**.

![[Pasted image 20250811084916.png]]

4. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

## Step 4
### ⌨️ Activity: Generate release notes
1. In a separate tab, go to the **Releases** page for this repository.
    - _Tip: To reach this page, click the **Code** tab at the top of your repository. Then, find the navigation bar below the repository description, and click the **Releases** heading link._
2. Click the **Draft a new release** button.
3. In the field for _Tag version_, specify `v1.0.0`.

![[Pasted image 20250811085158.png]]

4. To the right of the tag dropdown, click the _Target_ dropddown and select the `release-v1.0` branch.
    - _Tip: This is temporary in order to generate release notes based on the changes in this branch._

![[Pasted image 20250811085227.png]]

5. To the top right of the description text box, click **Generate release notes**.
6. Review the release notes in the text box and customize the content if desired.

![[Pasted image 20250811085247.png]]

7. Set the _Target_ branch back to the `main`, as this is the branch you want to create your tag on once the release branch is merged.
8. Click **Save draft**, as you will publish this release in the next step.

![[Pasted image 20250811085323.png]]

You can now [merge](https://docs.github.com/en/get-started/quickstart/github-glossary#merge) your pull request!

### ⌨️ Activity: Merge into main

1. In a separate tab, go to the **Pull requests** page for this repository.
2. Open your **Release v1.0** pull request.
3. Click **Merge pull request**.
4. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

![[Pasted image 20250811085409.png]]

## Step 5
### ⌨️ Activity: Finalize release
1. In a separate tab, go to the **Releases** page for this repository.
    - _Tip: To reach this page, click the **Code** tab at the top of your repository. Then, find the navigation bar below the repository description, and click the **Releases** heading link._
2. Click the **Edit** button next to your draft release.
3. Ensure the _Target_ branch is set to `main`.
4. Click **Publish release**.

![[Pasted image 20250811085737.png]]

5. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

## Step 6
### ⌨️ Activity: Create and merge the hotfix pull request
1. Open a pull request with `hotfix-v1.0.1` as the `base` branch, and `fix-game-background` as the `compare` branch.
2. Fill in the pull request template to describe your changes. You can set the pull request title to "Hotfix for broken game style". You can include a detailed pull request body, an example is below:
    
    ```
    ## Description:
    - Fixed bug, set game background back to black
    ```

![[Pasted image 20250811085941.png]]

3. Review the changes and click **Create pull request**.

![[Pasted image 20250811090001.png]]

4. We want to merge this into our hotfix branch now so click **Merge pull request**.

![[Pasted image 20250811090033.png]]

### ⌨️ Activity: Create the release pull request
1. Open a pull request with `main` as the `base` branch, and `hotfix-v1.0.1` as the `compare` branch.
2. Ensure the title of your pull request is "Hotfix v1.0.1".
3. Include a detailed pull request body, an example is below:
    
    ```
    ## Description:
    - Fixed bug introduced in last production release - set game background back to black
    ```

![[Pasted image 20250811090215.png]]

4. Review the changes and click **Create pull request**.
5. Click **Merge pull request**.

![[Pasted image 20250811090256.png]]

6. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

## Step 7
### ⌨️ Activity: Complete release
1. In a separate tab, go to to the **Releases** page for this repository.
    - _Tip: To reach this page, click the **Code** tab at the top of your repository. Then, find the navigation bar below the repository description, and click the **Releases** heading link._
2. Click the **Draft a new release** button.
3. Set the _Target_ branch to `main`.
    - _Tip: Practice your semantic version syntax. What should the tag and title for this release be?_
4. To the top right of the description text box, click **Generate release notes**.

![[Pasted image 20250811090640.png]]

5. Review the release notes in the text box and customize the content if desired.
6. Click **Publish release**.

![[Pasted image 20250811090657.png]]

7. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.

Course ended: [JMMA86/skills-release-based-workflow: My clone repository](https://github.com/JMMA86/skills-release-based-workflow)
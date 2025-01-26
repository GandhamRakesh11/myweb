To set up an end-to-end CI/CD pipeline using Jenkins, Maven, and Git for your project, you can follow these general steps. The goal is to automate the process of building, testing, and deploying the application whenever new code is pushed to your Git repository.

Prerequisites:
Jenkins: Installed and running.
Maven: Installed and configured on the Jenkins server.
Git: Installed and configured on the Jenkins server.
GitHub/Bitbucket/other Git repository: Your project repository.
Steps to Set Up the CI/CD Pipeline:
1. Create a New Jenkins Job:
Open your Jenkins dashboard.
Click on New Item.
Choose Freestyle project and name it (e.g., my-ci-cd-project).
Click OK.
2. Configure Git for the Jenkins Job:
In your project configuration page, under the Source Code Management section, select Git.
Enter the Git repository URL (for example, https://github.com/user/project.git).
If your repository is private, add credentials to Jenkins to allow access. You can add these credentials under Manage Jenkins > Manage Credentials.
3. Set Up Build Triggers (Optional):
In the Build Triggers section, select how you want Jenkins to trigger the build. A common choice is:
Poll SCM: Jenkins will check for changes in the Git repository periodically (e.g., every minute).
GitHub hook trigger for GITScm polling: This will trigger the build when changes are pushed to the Git repository. This requires setting up a webhook in your GitHub repository.
4. Configure the Build Environment:
In the Build Environment section, you can set things like Maven and JDK to use for the build process.
Set the JDK: Under Build Environment, choose the correct JDK to be used.
Set the Maven Version: Ensure that Maven is installed and select the appropriate version from the drop-down.
5. Add Build Step to Execute Maven:
In the Build section, click Add build step and select Invoke top-level Maven targets.
In the Goals field, enter the Maven command that will build the project (e.g., clean install).
clean: Cleans up the target directory before building.
install: Compiles the code and installs the artifact to the local Maven repository.
You can also configure additional Maven goals, such as running tests (clean test), if needed.
6. Post-build Actions (Optional):
You can configure post-build actions to define what happens after the build completes.
Archive the artifacts: To store the build output, such as the .jar or .war file, you can archive it in Jenkins.
Send notifications: Configure email notifications or integrate Slack for notifications about the build result.
Example configuration for archiving build artifacts:

In the Post-build Actions section, click Add post-build action and choose Archive the artifacts.
In the Files to archive field, you can specify the paths to the files you want to archive (e.g., target/*.jar or target/*.war).
7. Run the Jenkins Job:
After saving your Jenkins job, click Build Now to start the process.
Jenkins will clone the Git repository, run Maven to build and test the project, and display the results in the build console output.
8. Optional: Set Up Deployment:
After the build process completes successfully, you may want to deploy the artifact (e.g., .jar, .war) to a server or cloud environment as part of your CI/CD pipeline.

For example:

Deploy to a server: Use a post-build action to deploy the artifact to a server (via SCP, FTP, or other deployment tools).
Deploy to Cloud: Use Jenkins plugins to integrate with cloud services (e.g., AWS, Azure, or Google Cloud) for automatic deployment.

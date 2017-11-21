# Job-Match
Watson Personality insight job Match


Prerequisites

1.	An IBM Cloud account. The account is free and provides access to everything you need to develop, track, plan, and deploy apps. Sign up for a trial. The account requires an IBMid. If you don't have an IBMid, you can create one when you register.
2.	A GitHub account. If you don't have one, sign up.
3.	Verify the toolchains and tool integrations that are available in your region and IBM Cloud environment. A toolchain is a set of tool integrations that support development, deployment, and operations tasks.
3.	

Task 1: Create a toolchain

1.	Open the creation page for the Simple Cloud Foundry toolchain by clicking the Create toolchain button. 
 
Tip: For instructions to navigate to the toolchain templates and select a toolchain to create, see Navigating to the toolchain templates.
2.	On the creation page, review the diagram of the toolchain that you are about to create. The diagram shows each tool integration in its lifecycle phase in the toolchain.
 
3.	Review the default information for the toolchain settings. The toolchain's name identifies it in IBM Cloud. Toolchains are defined across an org. If you want to use a different org or name, change them.
4.	If you haven't authorized with GitHub, you are prompted to do so. Click Authorize and follow the instructions to link your IBM Cloud account to a GitHub account.
 
5.	Review your GitHub settings and, if needed, change them. Each toolchain comes with a sample app, but you can select another repo to use.
 
o	To enable issue tracking for ideas, enhancements, tasks, or bugs, select the Enable GitHub Issues check box.
o	To track the deployment of code changes by creating tags, labels, and comments on commits, pull requests, and referenced issues, select the Select Track deployment of code changes check box.
6.	Click Create. Several steps run automatically to set up your toolchain:
o	The toolchain is created.
o	The delivery pipeline is created and triggered.
o	The sample repo is cloned into your GitHub account.
o	The toolchain is associated with your app. When you push changes to the toolchain's GitHub repo, the pipeline automatically builds and deploys the app.
After a few moments, your new toolchain's Overview page opens.
 
 
How easy or difficult was it to link your IBM Cloud account to a GitHub account? 
•  Add comments ... 
•  You can see the deployed app by clicking View App.
 
Note: If you do not see a route when you click the arrow on the View App button, either the pipeline is not finished deploying or an error occurred while your app was being deployed. Click Delivery Pipeline to see the status of the deployment. To debug pipeline issues, see Troubleshooting Continuous Delivery issues.
The running app is displayed.
 
•  Return to the Toolchains page.
 
The Toolchains page displays all the toolchains that are in your org. For each toolchain, you can see icons that represent the tool integrations that are in that toolchain. From this list, you can rename and delete toolchains.
•  Click your new toolchain to open its Overview page.
Task 2: Modify the code
In this tutorial, you use the Eclipse Orion Web IDE to modify source code. When you edit in the Web IDE, your changes are saved to your cloud workspace. When you commit a change, it is saved to a Git repo on the cloud. When you push or sync a change, it is pushed to the origin Git repo (remote repo). Syncing a change also saves the change from the remote repo to your Git repo and workspace on the cloud.
You can also use the GitHub editor or your favorite editor to modify your app's code.
1.	On the toolchain's Overview page, click Eclipse Orion Web IDE. Your GitHub repo is automatically loaded in your workspace. The name of the repo that is shown in the file navigator is the name that you specified for the sample GitHub Enterprise repo when you created the toolchain.
Tip: If you completed this tutorial more than once, your workspace might contain multiple GitHub repos. The repo for the current toolchain is highlighted.
 
2.	In the file navigator, expand the repo for your current toolchain and go to the index.html file in the public folder.
 
3.	In the file directory, click index.html to open the file.
 
4.	Edit the h1 text to change the text that is displayed by the deployed app. Your changes are automatically saved.
 
5.	Push your changes:
a. From the Eclipse Orion Web IDE menu, click the Git icon.
 
b. In the Working Directory Changes section, type a commit message and make sure that the changed file is selected. You can expand public/index.html to see the changes. The changes are highlighted: the original content is in red and the changed content is in green.  
c. Click Commit to put the changes in the local master branch.
d. To push the changes to the origin/master branch, click Push. The origin/master branch is used by the pipeline, which automatically builds and deploys your changes.
 
 
How easy or difficult was it to commit changes to your local branch and then push them to the origin/master branch?
•  Add comments ... 
•  Return to the toolchain's Overview page by clicking the Back to DevOps arrow.
 
•  Click Delivery Pipeline to watch the stages run in response to your commit.
•  When the pipeline process is completed, go to your toolchain's Overview page and click View App.
 
•  Verify that your changes are visible in the running app.
 
 
Task 3: Add a stage to the pipeline

1.	Click on the toolchain's Overview page.
 
2.	Click on the Delivery Pipeline tool integration to view the build and deployment activity for your app. The pipeline has two stages: one where your app is built and another where it is deployed. After the pipeline completes its deployment process, the pipeline dashboard shows that both stages completed successfully.
 
The Build stage contains a build job that compiles your project in preparation for deployment. The Simple builder type packages your app, expecting the code to be in the root folder. If you use any other builder type, the build stage compiles your app, builds it, or both. This job generates artifacts that can be sent to a build archive directory. However, by default, the artifacts are placed in the project's root directory. 
The Deploy stage contains a deploy job that deploys the artifacts created by the Build stage. If a manifest file in the root folder exists, it is used to determine which buildpack to use. For more information about pipeline stages, see the IBM Cloud Docs.
3.	To add a third stage to deploy a test instance of your app, click Add Stage.
4.	Click the stage name, MyStage, and change the name to Deploy Stage - Test.
 
5.	Click the JOBS tab.

6.	Click ADD JOB, and then select the Deploy job type.
 
7.	Review the values that are specified in the Organization and Space fields. Those values specify the org and space that the test instance of the app is deployed to. Make sure that a valid org and space are selected.
 
8.	In the Deploy Script field, change the cf push command to cf push "${CF_APP}"-test -n "${CF_APP}"-test. Note that this stage is configured to stop if the job fails. Also, by default, only developers who are members of the targeted space have permission to run the stage. 
This command will deploy the app to the test server.
 
9.	Click SAVE.
10.	Drag the stage that you just created so that it is between the first two stages.
 
11.	View the updated pipeline.
 
12.	Click on the Run Stage button in the new stage.
 
13.	See the pipeline after all three stages run.
 
Note: For the new stage, the app name is simple-toolchain-tut-test. That name is set by the push "${CF_APP}"-test command . The deployed app is running at the simple-toolchain-tut-test.mybluemix.net route, which is set by the -n attribute that sets the host name.


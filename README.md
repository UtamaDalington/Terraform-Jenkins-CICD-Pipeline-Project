## Terraform CI/CD Automation With Jenkins
![DevelopmentEnvironmentSetupProject!](https://lucid.app/publicSegments/view/5d5293df-a178-4dae-bd63-7d63aed404bc/image.png)

###### Project ToolBox 🧰
- [Git](https://git-scm.com/) Git will be used to manage our application source code.
- [Github](https://github.com/) Github is a free and open source distributed VCS designed to handle everything from small to very large projects with speed and efficiency.
- [Jenkins](https://www.jenkins.io/) Jenkins is an open source automation CI tool which enables developers around the world to reliably build, test, and deploy their software.
- [Snyk](https://snyk.io/) Snyk gives you the visibility, context, and control you need to work alongside developers on reducing application risk. 
- [Checkov](https://www.checkov.io/) Checkov scans cloud infrastructure configurations to find misconfigurations before they're deployed.
- [Slack](https://slack.com/) Slack is a communication platform designed for collaboration which can be leveraged to build and develop a very robust DevOps culture. Will be used for Continuous feedback loop.

1) Create a GitHub Repository with the name `Terraform-CICD-Pipeline-Project` and push the code in this branch(main) to 
    your remote repository (your newly created repository). 
    - Go to GitHub: https://github.com
    - Login to `Your GitHub Account`
    - Create a Repository called `Terraform-CICD-Pipeline-Project`
    - Clone the Repository in the `Repository` directory/folder on your `local machine`
    - Download the code in in this repository `"Main branch"`: https://github.com/UtamaDalington/Terraform-Jenkins-CICD-Pipeline-Project.git
    - `Unzip` the `code/zipped file`
    - `Copy` and `Paste` everything `from the zipped file` into the `repository you cloned` in your local
    - Open your `Terminal`
        - Add the code to git, commit and push it to your upstream branch "main or master"
        - Add the changes: `git add -A`
        - Commit changes: `git commit -m "adding project source code"`
        - Push to GitHub: `git push`
    - Confirm that the code is now available on GitHub as shown below...
    <img width="1920" height="932" alt="Screenshot (328)" src="https://github.com/user-attachments/assets/2efcced3-544b-4d5c-94d0-bd811e5e7579" />


2) Create An IAM Profile/Role For The Jenkins Environment
- Create an EC2 Service Role in IAM with `AdministratorAccess` Privilege 
- Navigate to IAM
<img width="1920" height="872" alt="Screenshot (331)" src="https://github.com/user-attachments/assets/6a4930c1-0488-493f-849d-6cc38c97d7d0" />

    - Click on `Roles`
    - Click on `Create Role`
    - Select `Service Role`
    - Use Case: Select `EC2`
    - Click on `Next` 
    - Attach Policy: `AdministratorAccess`
    - Click `Next` 
    - Role Name: `AWS-AdministratorAccess-Role`
    - Click `Create`

3) Jenkins
    - Create a Jenkins VM instance 
    - Name: `Jenkins-CI`
    - AMI: `Ubuntu 24.04`
    - Instance type: `c7i-flex.large (2 vCPU and 4 GiB Memory)`
    - Key pair: `Select` or `create a new keypair`
    - Security Group (Edit/Open): `8080` and `22` to `0.0.0.0/0`
    - IAM instance profile: Select the `AWS-AdministratorAccess-Role`
    - User data (Copy the following user data): https://github.com/UtamaDalington/Maven-SonarQube-Nexus-Jenkins-installations/blob/main/terraform-jenkins.sh
    - Launch Instance
    <img width="1426" height="1040" alt="Screenshot (330)" src="https://github.com/user-attachments/assets/85644107-3cc0-491e-b332-5e7032cea846" />


4) Slack 
    - Go to Slack, create a `Workspace` and give it a name (for example: `CICD-Pipeline-Peojects`)
      - Create a `Private Channel` using the naming convention `YOUR_INITIAL-terraform-cicd-alerts`
        - **NOTE:** *`(The Channel Name Must Be Unique, meaning it must be available for use)`*
      - Visibility: Select `Private`
      - Click on the `Channel Drop Down` and select `Integrations` and Click on `Add an App`
      - Search for `Jenkins` and Click on `View`
      - Click on `Configuration/Install` and Click `Add to Slack` 
      - On Post to Channel: Click the Drop Down and select your channel above `YOUR_INITIAL-terraform-cicd-alerts`
      - Click `Add Jenkins CI Integration`
      - Scroll Down and Click `SAVE SETTINGS/CONFIGURATIONS`
      - Leave this page open
      <img width="1600" height="862" alt="Screenshot (1)" src="https://github.com/user-attachments/assets/2c266576-871b-485b-b786-d98378864f59" />

5) Install Plugins
- Snyk 
- Slack
- Blue Ocean
- Pipeline: Stage View


## How to setup for Shared Library

- Configure Jenkins Global Pipeline Library
Go to Jenkins UI:

- Navigate to Manage Jenkins > Configure System.
Add the Shared Library:

- Scroll down to the Global Pipeline Libraries section.
Click Add to add a new library.
- Configure the Library:

Name: Enter the name of your library (e.g., my-jenkins-library).
Source Code Management: Select Git.
Repository URL: Enter the URL of your Git repository, like https://github.com/anumcait/devops-learning-journey.git.
Credentials: If the repository is private, select or add credentials (e.g., GitHub personal access token or SSH key).
Branch: Set the branch name (e.g., main).

**Note **
If any one create a sub folder for jenkins library (like me), you will get error while building.

I googled and found solution. Below is the solution

![image](https://github.com/user-attachments/assets/c577b1a2-933c-47f4-bd9e-53f7c55e230c)
![image](https://github.com/user-attachments/assets/e3d71188-8507-4be7-af26-740d436c7795)

- Mention sub folder in the Library path at the bottom of the Global Trusted Pipeline Libraries. (default ./ will be existed, change to ./<<your_custom_folder>>
- Ex: ./jenkins

Finally your folder structure look like this:
devops-learning-journey/
├── jenkins/
│   └── vars/
│       └── myVar.groovy  <-- Your Groovy file here

Automating a release process through CI/CD -

<img width="1238" height="407" alt="image" src="https://github.com/user-attachments/assets/b3d21086-f5e8-4550-bb87-22fc36a0899f" />

Here the CI job ends and CD job gets triggered automatically.
Our CD job will first update the build number and relese number in deployment.yaml in the gitOps repo in the github, then ArgoCD will pull the manifest file and deploy the resources on the EKS cluster.

once the CD job is finished it will send the notification over slack and send the email as well.

register-app
<br>
Test93


Instructions
============

Create and run Blazor app
=========================
- Create the folder and move into it.
- Create the Blazor app.
  - dotnet new blazorserver -o BlazorServerApp
- Move into the BlazorServerApp project folder.
- Build the project
  - dotnet build
- Run the project and make sure app runs at the URL specified.
  - dotnet run
- Now it's time to add the project to GitHub.

Azure Resources
===============
- Create a Resource Group called "ff-conapp-rg" in UK South region.
- Create a Standard Container Registry (ACR) called "ffacr33" in UK South region.
- Once the ACR is created get its URL in "Access Keys" section => ffacr33.azurecr.io.
- Once the image is pushed to ACR, create the Container App => myblazorapp. Make sure to use ACR and image:tag during the creation in app settings. Also accept traffic from anywhere and use the container port specified in dockerfile. Once deployed app should be available via container app URL.

Dockerize the project and push to ACR
=====================================
- Open project in VS Code.
- Add a Linux dockerfile via VS Code command pallette.
  - (Command + Shipt + P) => Docker: Add Docker Files to Workspace.
- Also add a .gitignore file using VS Code command pallette.
- Open a new terminal in VS Code and make sure you're inside the solution folder.
- Build the Docker image for the app.
  - docker build . -t blazorserverapp:latest -f Dockerfile
- Make sure the image is built.
  - docker images
- Tag the image with ACR URL.
  - docker tag blazorserverapp:latest ffacr33.azurecr.io/blazorserverapp:latest
- Make sure the tagging has worked.
  - docker images
- Login to the ACR.
  - az acr login --name ffacr33
- Push the newly tagged image to ACR.
  - docker push ffacr33.azurecr.io/blazorserverapp:latest
- Visit the ACR on Azure and make sure the image is available there.
- Make sure the Admin user is enabled in ACR.

Setup CI/CD for the Container App
=================================
- Visit "Continuous deployment" blade of Container App on Azure Portal.
- Click on the "Sign in with GitHub" link on the page and authorise to use GitHub.
- Select the "master/main" branch of the project repository.
- Click on the "Configure service principal" link and create an associated service principal.
- Finally, click on "Start continuous deployment" button at the bottom.
- Notice the new ".github/workflows/" folder and the CI/CD YAML file created in GitHub repository.
- Click on "Actions" tab and make sure the build/deploy runs correctly. Fix any build/deploy issues that may exist.
- Notice the new Repository created in ACR and images are added along with the tags.
- Now, it's time to pull the CI/CD pipeline changes to local Git repository.
  - git pull
- Do a small change to "Pages/Index.razor" file and push the change. Make sure change is visible in  Azure Container App after the completion of the CI/CD pipeline.
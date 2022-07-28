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

Azure Resources
===============
- Create a Resource Group called "ff-conapp-rg" in UK South region.
- Create a Standard Container Registry (ACR) called "ffacr33" in UK South region.
- Once the ACR is created get its URL in "Access Keys" section => ffacr33.azurecr.io

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
- 
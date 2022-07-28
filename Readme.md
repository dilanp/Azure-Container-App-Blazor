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
- Once the ACR is created 

Dockerize the project and push to ACR
=====================================
- Open project in VS Code.
- Add a Linux dockerfile via VS Code command pallette 
  - (Command + Shipt + P) => Docker: Add Docker Files to Workspace.
- 
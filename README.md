# DanielCarey.SlnPlus

This is my ```dotnet new slnplus``` template for configuring my initial development folder. It is based on my linqpad snippet below. I decided to automate this setup instead of copying and pasting from that snippet each time I start a new project.

Here are some features of using this tool:
* Enforces extremely strict compiler analysis including treating warnings as errors for projects added in the .\src\ folder.
* Creates a default ```.editorconfig``` file to enforce a default syntax standard. This sets generated namespaces to use file-scoped instead of block-scoped.

The default compiler checks are **very strict** and can be relaxed by modifying the ```./src/Directory.Build.props``` file. See this document for changing the settings. [Configuration options for code analysis]( https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/configuration-options )

## Install and Uninstall from source

```powershell
# Install
dotnet new install ./working/content/SlnPlus
# Uninstall
dotnet new uninstall ./working/content/SlnPlus
```

## Build template package and install

```powershell
# Package template
dotnet pack .\working\DanielCarey.SlnPlus.csproj -o ./dist
# Install package
dotnet new install .\dist\DanielCarey.SlnPlus.1.0.0.nupkg
# Uninstall template
dotnet new uninstall DanielCarey.SlnPlus
```

## After Installation

1. Create a folder for the new solution
1. Run snippet *```dotnet new slnplus```*

## Original LINQPad Snippet
```
/05 - Playbooks/01 - Project Settings and Creation.linq
```

```csharp

```powershell
$framework = "net8.0"
$sdkVersion = "8.0.302"
$solutionName = "DanielCarey.SlnPlus"

mkdir src
dotnet new gitignore
dotnet new globaljson --sdk-version $sdkVersion
dotnet new editorconfig
dotnet new sln -n "$solutionName"
dotnet new buildprops -o src\
dotnet new buildtargets -o src\
git init
git add .
git commit -m 'Initial project'

# Console
$projectName = "console"
$projectName = if(($x = Read-Host "$projectName") -eq ''){"$projectName"} else {$x} # allow prompt repalce
dotnet new console -o src/"$projectName" -f $framework --aot
dotnet sln "$solutionName.sln" add src/"$projectName"/"$projectName".csproj

# Aspire
dotnet new aspire -n "$solutionName" -o src/ -f $framework
rm src/"$solutionName.sln"
dotnet sln "$solutionName.sln" add src/"$solutionName.AppHost"/"$solutionName.AppHost".csproj
dotnet sln "$solutionName.sln" add src/"$solutionName.ServiceDefaults"/"$solutionName.ServiceDefaults".csproj

# WebApi
$projectName = "webapi"
$projectName = if(($x = Read-Host "$projectName") -eq ''){"$projectName"} else {$x} # allow prompt repalce
dotnet new webapi -o src/"$projectName" -f $framework  # --no-openapi
dotnet sln "$solutionName.sln" add src/"$projectName"/"$projectName".csproj

# Blazor App
$projectName = "blazor"
$projectName = if(($x = Read-Host "$projectName") -eq ''){"$projectName"} else {$x} # allow prompt repalce
dotnet new blazor -o src/"$projectName" -f $framework --interactivity auto
dotnet sln "$solutionName.sln" add src/"$projectName"/"$projectName"/"$projectName".csproj
dotnet sln "$solutionName.sln" add src/"$projectName"/"$projectName".Client/"$projectName".Client.csproj

# ===MyTemplates===

# Blazor Plus
$projectName = "blazorplus"
$projectName = if(($x = Read-Host "$projectName") -eq ''){"$projectName"} else {$x} # allow prompt repalce
dotnet new blazorplus -o src/"$projectName"
dotnet sln "$solutionName.sln" add src/"$projectName"/"$projectName"/"$projectName".csproj
dotnet sln "$solutionName.sln" add src/"$projectName"/"$projectName".Client/"$projectName".Client.csproj

# BabylonJS
$projectName = "babylonjs"
$projectName = if(($x = Read-Host "$projectName") -eq ''){"$projectName"} else {$x} # allow prompt repalce
dotnet new babylonjs -o src/"$projectName"
dotnet sln "$solutionName.sln" add src/"$projectName"/"$projectName".csproj

git add .
git commit -m 'Added projects'

```

## References

[Configuration options for code analysis]( https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/configuration-options )

[MSBuild reference for .NET SDK projects - Analysis Mode]( https://docs.microsoft.com/en-us/dotnet/core/project-sdk/msbuild-props#analysismode )

[dotnet templating]( https://github.com/dotnet/templating/wiki )

[template.json reference]( https://github.com/dotnet/templating/wiki/Reference-for-template.json )

[Template for 'dotnet new sln']( https://github.com/dotnet/sdk/tree/main/template_feed/Microsoft.DotNet.Common.ItemTemplates/content/Solution )





# DanielCarey.SlnPlus

My default solution folder configuration based on my LINQPad snippet:

```
/05 - Playbooks/01 - Project Settings and Creation.linq
```


## Install/Uninstall

```powershell
dotnet new install .
dotnet new slnplus
dotnet new uninstall .
```

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


---
title: IIS Web App Deploy task
description: Deploy a website or web app using WebDeploy
ms.topic: reference
ms.assetid: 1B467810-6725-4B6D-ACCD-886174C09BBA
ms.custom: seodec18
ms.author: ronai
author: RoopeshNair
ms.date: 12/07/2018
monikerRange: 'azure-devops'
---

# IIS Web App Deploy task

[!INCLUDE [version-eq-azure-devops](../../../includes/version-eq-azure-devops.md)]

Use this task to deploy a website or web app using WebDeploy.

::: moniker range="> tfs-2018"

## YAML snippet

[!INCLUDE [temp](../includes/yaml/IISWebAppDeploymentOnMachineGroupV0.md)]

::: moniker-end

## Arguments

<table><thead><tr><th>Argument</th><th>Description</th></tr></thead>
<tr><td>Website Name</td><td>(Required) Provide the name of an existing website on the machine group machines</td></tr>
<tr><td>Virtual Application</td><td>(Optional) Specify the name of an already existing Virtual Application on the target Machines</td></tr>
<tr><td>Package or Folder</td><td>(Required) File path to the package or a folder generated by MSBuild or a compressed archive file.<br />Variables ( <a href="/azure/devops/pipelines/process/variables" data-raw-source="[Build](../../process/variables.md)">Build</a> | <a href="/azure/devops/pipelines/build/variables" data-raw-source="[Release](../../build/variables.md)">Release</a>), wild cards are supported. <br/> For example, $(System.DefaultWorkingDirectory)*<em>*.zip.</td></tr>
<tr><td>SetParameters File</td><td>(Optional) Optional: location of the SetParameters.xml file to use.</td></tr>
<tr><td>Remove Additional Files at Destination</td><td>(Optional) Select the option to delete files on the Web App that have no matching files in the Web App zip package.</td></tr>
<tr><td>Exclude Files from the App_Data Folder</td><td>(Optional) Select the option to prevent files in the App_Data folder from being deployed to the Web App.</td></tr>
<tr><td>Take App Offline</td><td>(Optional) Select the option to take the Web App offline by placing an app_offline.htm file in the root directory of the Web App before the sync operation begins. The file will be removed after the sync operation completes successfully.</td></tr>
<tr><td>Additional Arguments</td><td>(Optional) Additional Web Deploy arguments that will be applied when deploying the Azure Web App like,-disableLink:AppPoolExtension -disableLink:ContentExtension.</td></tr>
<tr><td>XML transformation</td><td>(Optional) The config transforms will be run for <code></em>.Release.config</code> and <code><em>.&lt;stageName&gt;.config</code> on the <code></em>.config file</code>.<br/> Config transforms will be run prior to the Variable Substitution.<br/>XML transformations are supported only for Windows platform.</td></tr>
<tr><td>XML variable substitution</td><td>(Optional) Variables defined in the Build or Release Pipeline will be matched against the &#39;key&#39; or &#39;name&#39; entries in the appSettings, applicationSettings, and connectionStrings sections of any config file and parameters.xml. Variable Substitution is run after config transforms. <br/><br/> Note: If the same variables are defined in the release pipeline and in the stage, the stage variables will supersede the Release Pipeline variables.<br/></td></tr>
<tr><td>JSON variable substitution</td><td>(Optional) Provide new line separated list of JSON files to substitute the variable values. Files names are to be provided relative to the root folder. <br/> To substitute JSON variables that are nested or hierarchical, specify them using JSONPath expressions. <br/> <br/> For example, to replace the value of ‘ConnectionString’ in the sample below, you need to define a variable as ‘Data.DefaultConnection.ConnectionString’ in the build/release pipeline (or release pipeline&#39;s stage). <br/> {<br/>&nbsp;&nbsp;&quot;Data&quot;: {<br/>&nbsp;&nbsp;&nbsp;&nbsp;&quot;DefaultConnection&quot;: {<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;ConnectionString&quot;: &quot;Server=(localdb)\SQLEXPRESS;Database=MyDB;Trusted_Connection=True&quot;<br/>&nbsp;&nbsp;&nbsp;&nbsp;}<br/>&nbsp;&nbsp;}<br/> }<br/> Variable Substitution is run after configuration transforms. <br/><br/> Note: Build/release pipeline variables are excluded in substitution</td></tr>
</table>

### [Task control options](../../process/tasks.md#controloptions)

## Open source

This task is open source [on GitHub](https://github.com/Microsoft/azure-pipelines-tasks). Feedback and contributions are welcome.
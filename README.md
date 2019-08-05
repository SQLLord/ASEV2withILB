App Service Environment with Website
------------------------------------

This template illustrates how to deploy [Azure App Service Environment](https://docs.microsoft.com/en-us/azure/app-service/environment/intro) a.k.a. ASEv2 with ILB configuration.

The template allows you to supply an existing Subnet for ASE deployment (there should be no resources in this Subnet). If you do not supply a Subnet, i.e. leave that parameter as `null`, a new Virtual Network will be created and the ASE deployed in it. 

The ASE needs a certificate, which supports the `*.domainname`, and `*.scm.domainname` DNS names. If you do not have a certificate, you can generate one with the `New-SelfSignedCertificate` command. The repository also includes a [convenience script](https://github.com/SQLLord/ASEV2withILB/blob/master/Scripts/PrepareAseDeployment.ps1), that prepares the details needed for this deployment. To use the script for this deployment:

```
scripts\PrepareAseDeployment.ps1 -DomainName mydomain-internal.us -OutFile C:\temp\myase.parameters.json
```

This will generate a parameter file that you can use to either copy/paste from or with a CLI or Powershell command to deploy the template. 

Note: It would be possible (and better) to deploy the certificate using Key Vault, but this workflow is not supported in all clouds (including sovereign clouds); for compatibility reasons, the certificate is passed as a string blob in this template.

<a href="https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSQLLord%2FASEV2withILB%2Fblob%2Fmaster%2Fazuredeploy.json" target="_blank">
<img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazuregov.png"
</a>
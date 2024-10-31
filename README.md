# azure-management
Convenient scripts for accomplishing common tasks within business organizations

# Azure PowerShell Setup Guide

This guide walks through the process of setting up PowerShell for Azure management.

## Prerequisites
- Windows PowerShell 5.1+ or PowerShell Core 7.x+
- Administrator access to your machine
- Azure subscription with appropriate permissions

## Installation Steps

### 1. Install PowerShell (if not already installed)
#### Windows
PowerShell comes pre-installed on Windows. To install the latest version:
```powershell
winget install Microsoft.PowerShell
```

#### macOS
```bash
brew install powershell
```

#### Linux (Ubuntu)
```bash
# Install system components
sudo apt-get update
sudo apt-get install -y wget apt-transport-https software-properties-common

# Download Microsoft repository GPG keys
wget -q "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb"

# Register Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update package list and install PowerShell
sudo apt-get update
sudo apt-get install -y powershell
```

### 2. Install Azure PowerShell Module
```powershell
# Install the Az module
Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force

# Import the module
Import-Module Az
```

### 3. Connect to Azure
```powershell
# Connect to Azure interactively
Connect-AzAccount

# If you have multiple subscriptions, select the one you want to use
Set-AzContext -SubscriptionId "<subscription-id>"
```

### 4. Verify Installation
```powershell
# Check Az module version
Get-Module Az -ListAvailable

# Test Azure connection
Get-AzSubscription
```

## Common Issues and Solutions

### SSL/TLS Security Protocol
If you encounter SSL/TLS errors:
```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```

### Module Import Failures
If you encounter module import failures:
```powershell
# Clear PowerShell session state
Remove-Module Az* -Force
# Reinstall Az module
Install-Module -Name Az -Force -AllowClobber
```

### Authentication Issues
If you encounter authentication issues:
1. Clear Azure credentials:
```powershell
Clear-AzContext
```
2. Reconnect:
```powershell
Connect-AzAccount
```

## Best Practices
1. Keep PowerShell and Az module updated
2. Use service principals for automated scripts
3. Store credentials securely
4. Use appropriate RBAC roles

## Additional Resources
- [Official Azure PowerShell Documentation](https://docs.microsoft.com/en-us/powershell/azure/)
- [Azure PowerShell Sample Scripts](https://docs.microsoft.com/en-us/azure/samples/)
- [PowerShell Gallery](https://www.powershellgallery.com)

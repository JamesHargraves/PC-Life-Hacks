---
title: Update Drivers
---

# Ensure this script is run as Administrator
if (-not ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole("Administrator")) {
    Write-Error "Please run this script as Administrator."
    exit
}

# Update all present PnP devices' drivers automatically
Get-PnpDevice -PresentOnly | ForEach-Object {
    Write-Host "Updating driver for:" $_.FriendlyName
    try {
        Update-PnpDevice -InstanceId $_.InstanceId -Force -Confirm:$false
    }
    catch {
        Write-Warning "Could not update driver for: $($_.FriendlyName)"
    }
}

---

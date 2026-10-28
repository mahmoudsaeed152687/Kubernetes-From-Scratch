# Kubernetes-From-Scratch

Install kubectl :

1. Change to Downloads >>>> cd "$HOME\Downloads"

2. Download kubectl >>>> curl.exe -LO "https://dl.k8s.io/release/v1.34.0/bin/windows/amd64/kubectl.exe"
 
3. Verify the downloaded file >>>> .\kubectl.exe version --client
 
4. Install it so you can run kubectl from anywhere >>>> New-Item -Path "C:\kubectl" -ItemType Directory -Force

Copy-Item "$HOME\Downloads\kubectl.exe" "C:\kubectl\kubectl.exe" -Force

5. Add it to the system path >>>> $machinePath = [Environment]::GetEnvironmentVariable("Path", "Machine")

if (($machinePath -split ';') -notcontains 'C:\kubectl') {
    [Environment]::SetEnvironmentVariable(
        "Path",
        "$machinePath;C:\kubectl",
        "Machine"
    )
}

6. Close and reopen PowerShell, then verify >>>> kubectl version --client


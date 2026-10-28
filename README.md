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
----------------------------------------------------------------------------------------------------
Install Kind on Windows using PowerShell:

1. Download Kind from GitHub >>>> curl.exe -L --fail --retry 3 `
  -o "$HOME\Downloads\kind.exe" `
  "https://github.com/kubernetes-sigs/kind/releases/download/v0.33.0/kind-windows-amd64"

2. Move Kind to your tools directory >>>> New-Item -Path "C:\kubectl" -ItemType Directory -Force

Move-Item "$HOME\Downloads\kind.exe" "C:\kubectl\kind.exe" -Force

3. Add C:\kubectl to your user PATH >>>> $userPath = [Environment]::GetEnvironmentVariable("Path", "User")

if (($userPath -split ';') -notcontains 'C:\kubectl') {
    $newPath = (@($userPath, 'C:\kubectl') | Where-Object { $_ }) -join ';'
    [Environment]::SetEnvironmentVariable("Path", $newPath, "User")
}

$env:Path += ";C:\kubectl"

4. Verify the installation >>>> kind version

5. Create a local Kubernetes cluster (Ensure Docker Desktop is running) >>>> kind create cluster --name devops-lab

6. Verify the cluster >>>> kubectl get nodes
kubectl get pods -A





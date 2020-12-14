# Ejercicio sobre servicios
## Obtener información sobre servicios:
### Ver estado de servicios
```powershell
Get-WmiObject -Class Win32_Service | Select-Object name, state
```
### Ver servicios que están "Running" (En ejecución)
```powershell
Get-WmiObject -Class Win32_Service | Where-Object State -EQ 'Running'
```
### Ver servicios que están "Stopped" (Parados)
```powershell
Get-WmiObject -Class Win32_Service | Where-Object State -EQ 'Stopped'
```
### Mostrar los procesos que se están ejecutando en relación con los servicios
```powershell
(Get-WmiObject -Class Win32_Service | Where-Object State -EQ 'Running') | %{
Write-Host $_.Name,$_.ProcessId,$_.State,(Get-Process -Id $_.ProcessId).Name
}
```
### Mostrar los servicios que se están ejecutando en relación con los procesos y los hilos
```powershell
(Get-WmiObject -Class Win32_Service | Where-Object State -EQ ‘Running’) | %{
Write-Host $_.Name,$_.ProcessId,$_.State,(Get-Process -Id $_.ProcessId).Name,(Get-WmiObject -Class Win32_Thread | Where-Object ProcessHandle -EQ $_.ProcessId)
}
```
### Mostrar los servicios que se están ejecutando en relación con los procesos y los hilos
```powershell
$i=0
(Get-WmiObject -Class Win32_Thread) | %{
$i++
Write-Host $i,$_.Handle,$_.ProcessHandle,(Get-WmiObject -Class Win32_Service | Where-Object State -EQ ‘Running’ | Where-Object ProcessId -EQ $_.ProcessHandle),(Get-Process -Id $_.ProcessHandle).ProcessName
}
``` 
### Mostrar información avanzada de los procesos (Path, ExecutablePath, CommandLine) que se están ejecutando en relación con los servicios
```powershell
(Get-WmiObject -Class Win32_Service | Where-Object State -EQ 'Running') |%{
Write-Host $_.Name,$_.ProcessId,$_.State,(Get-Process -Id $_.ProcessId | Select-Object name, Path, ExecutablePath, CommandLine)
Write-Host $_.Name,$_.ProcessId,$_.State,(Get-WmiObject -Class win32_process | Where-Object ProcessId -EQ  $_.ProcessId | select name, Path, ExecutablePath, CommandLine)
Write-Host "###---------------------INFORMACIÓN--------------------------###"
}

```

Add-Type -TypeDefinition @"
using System;
using System.Runtime.InteropServices;

public class PowerHelper {
    [DllImport("kernel32.dll", SetLastError = true)]
    public static extern uint SetThreadExecutionState(uint esFlags);
}
"@

# Evita suspensión y apagado de pantalla mientras PowerShell esté corriendo
[PowerHelper]::SetThreadExecutionState(0x80000002)

Write-Host "Sistema bloqueado de suspensión. Presiona Ctrl+C para salir y restaurar el comportamiento normal."

# Mantén el script vivo para que siga activo
while ($true) { Start-Sleep -Seconds 60 }

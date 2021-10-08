# Terminal GUI (TUI) für PowerShell

Angelegt von Jakob Heitzmann, zuletzt geändert am Jul 30, 2021

Tutorial: https://blog.ironmansoftware.com/tui-powershell/  
Github: https://github.com/migueldeicaza/gui.cs/tree/main/Terminal.Gui  
GitHub Overview (C#): https://migueldeicaza.github.io/gui.cs/articles/overview.html  
GitHub API Doc: https://migueldeicaza.github.io/gui.cs/api/Terminal.Gui/Terminal.Gui.html  

## Installation
Installation erfolgt über PowerShell.
Voraussetzung zur Nutzung ist eine aktuelle Version von PowerShell. 

> Install-Module Microsoft.PowerShell.ConsoleGuiTools
## Hello World Script
### Hello World
````PowerShell
Import-Module Microsoft.PowerShell.ConsoleGuiTools
$module = (Get-Module Microsoft.PowerShell.ConsoleGuiTools -List).ModuleBase
Add-Type -Path (Join-path $module Terminal.Gui.dll)
 
[Terminal.Gui.Application]::Init()
 
$W = [Terminal.Gui.Window]::new()
$W.Title = "Hello World"
 
[Terminal.Gui.Application]::Top.Add($W)
 
[Terminal.Gui.Application]::Run()
````
## Examples
### Example
````PowerShell
Import-Module Microsoft.PowerShell.ConsoleGuiTools
$module = (Get-Module Microsoft.PowerShell.ConsoleGuiTools -List).ModuleBase
Add-Type -Path (Join-path $module Terminal.Gui.dll)
 
[Terminal.Gui.Application]::Init()
 
$W = [Terminal.Gui.Window]::new()
$W.Title = "Example"
 
$BWidth = 20
$BX = 25
 
#Frames
 
$F1 = [Terminal.Gui.FrameView]::new()
$F1.Width = [Terminal.Gui.Dim]::Percent(50)
$F1.Height = [Terminal.Gui.Dim]::Fill()
$F1.Title = "Frame 1"
$W.Add($F1)
 
$F2 = [Terminal.Gui.FrameView]::new()
$F2.Width = [Terminal.Gui.Dim]::Percent(50)
$F2.Height = [Terminal.Gui.Dim]::Percent(50)
$F2.X = [Terminal.Gui.Pos]::Right($F1)
$F2.Title = "Frame 2"
$W.Add($F2)
 
##Frame 1
 
#Textfield
 
$L0 = [Terminal.Gui.Label]::new()
$L0.X = 0
$L0.Y = 0
$L0.Width = 10
$L0.Height = 1
$L0.Text = "Textfield"
$F1.Add($L0)
 
$TF0 = [Terminal.Gui.Textfield]::new()
$TF0.Text = ""
$TF0.Width = $BWidth
$TF0.X = $BX
$TF0.Y = 0
$F1.Add($TF0)
 
#ComboBox
 
$L2 = [Terminal.Gui.Label]::new()
$L2.X = 0
$L2.Y = 2
$L2.Width = 15
$L2.Height = 1
$L2.Text = "ComboBox"
$F1.Add($L2)
 
$CB0 = [Terminal.Gui.ComboBox]::new()
$CB0.X = $BX
$CB0.Y = 2
$CB0.Width = $BWidth
$CB0.Height = 4
$CB0.SetSource(@("Hallo!", "Moin", "Salle"))
$F1.Add($CB0)
 
#Checkbox
 
$ChB0 = [Terminal.Gui.Checkbox]::new()
$ChB0.X = 0
$ChB0.Y = 4
$ChB0.Checked = $true
$F1.Add($ChB0)
 
$L3 = [Terminal.Gui.Label]::new()
$L3.Text = "Checkbox"
$L3.X = [Terminal.Gui.Pos]::Right($ChB0)
$L3.Y = 4
$L3.Height = 1
$L3.Width = 20
$F1.Add($L3)
 
#Button
 
$BTN0 = [Terminal.Gui.Button]::New()
$BTN0.Text = "Button"
$BTN0.X = [Terminal.Gui.Pos]::AnchorEnd(11)
$BTN0.Y = [Terminal.Gui.Pos]::AnchorEnd(1)
$BTN0.add_Clicked({ [Terminal.Gui.MessageBox]::Query("MessageBox", "") })
$F1.Add($BTN0)
 
##Frame 2
 
$L4 = [Terminal.Gui.Label]::new()
$L4.X = [Terminal.Gui.Pos]::Center()
$L4.Y = [Terminal.Gui.Pos]::Center()
$L4.Width = 15
$L4.Height = 1
$L4.Text = "Label"
$F2.Add($L4)
 
##Fenster
 
$L5 = [Terminal.Gui.Label]::new()
$L5.X = [Terminal.Gui.Pos]::Right($F1) + 1
$L5.Y = [Terminal.Gui.Pos]::Bottom($F2)
$L5.Width = 15
$L5.Height = 1
$L5.Text = "Label"
$W.Add($L5)
 
[Terminal.Gui.Application]::Top.Add($W)
[Terminal.Gui.Application]::Run()
````
### Textfeld bei Änderung auslesen
````PowerShell
Import-Module Microsoft.PowerShell.ConsoleGuiTools
$module = (Get-Module Microsoft.PowerShell.ConsoleGuiTools -List).ModuleBase
Add-Type -Path (Join-path $module Terminal.Gui.dll)
  
[Terminal.Gui.Application]::Init()
  
$W = [Terminal.Gui.Window]::new()
$W.Title = "Example"
  
#Textfield
  
$TF0 = [Terminal.Gui.Textfield]::new()
$TF0.Text = ""
$TF0.Width = 20
$TF0.X = 0
$TF0.Y = 0
 
$L0 = [Terminal.Gui.Label]::new()
$L0.X = [Terminal.Gui.Pos]::Right($TF0) + 1
$L0.Y = 0
$L0.Width = 20
$L0.Height = 1
$L0.Text = ""
 
$TF0.add_TextChanged({ $L0.Text = -join [char[]]$TF0.Text })
 
 
$W.Add($TF0)
$W.Add($L0)
  
[Terminal.Gui.Application]::Top.Add($W)
[Terminal.Gui.Application]::Run()
````
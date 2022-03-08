# https://docs.microsoft.com/en-us/sysinternals/downloads/du
Function Get-DUDiskSize {
    param (
        $ComputerName = $env:COMPUTERNAME,
        $DuRunPath      = "c:\windows\temp\du.exe",
        [string[]]$Path
        )
    
        $DataObject = @()
        $BigFolderSizeData =  c:\windows\temp\du.exe -accepteula -nobanner -c -l 3 $Path | ConvertFrom-Csv | select $ComputerName, Path,@{Name="DirectorySize";expression={$_.DirectorySize / 1GB }} | Where-Object { $_.DirectorySize -gt 1 } | Sort-Object { $_.DirectorySize } -descending
        foreach($Folder in $BigFolderSizeData){
            $foldername = $Folder.path
            $foldersize= [System.Math]::Round(($Folder.DirectorySize))
            $Object = New-Object PSObject
            $Object | Add-Member -memberType NoteProperty -name Hostname -value $ComputerName
            $Object | Add-Member -memberType NoteProperty -name Foldername -value $foldername
            $Object | Add-Member -memberType NoteProperty -name FoldersizeGb -value $foldersize
            $DataObject += $Object
        }
        $DataObject

   
}
    
   
    
Get-DUDiskSize -Path C:\Windows
    

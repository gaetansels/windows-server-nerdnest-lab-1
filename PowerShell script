PS C:\WINDOWS\system32> Import-Module ActiveDirectory

# Pad naar het CSV-bestand
$csvPath = "C:\user-import\OUallusers.csv"

# Gebruikers toevoegen
Import-Csv -Path $csvPath | ForEach-Object {
    $firstName = $_.FirstName.Trim()
    $lastName = $_.LastName.Trim()
    $username = "$firstName.$lastName".ToLower()

    $securePass = ConvertTo-SecureString $_.Password -AsPlainText -Force
    New-ADUser `
        -Name "$firstName $lastName" `
        -GivenName $firstName `
        -Surname $lastName `
        -SamAccountName $username `
        -UserPrincipalName "$username@nerdnest.test" `
        -AccountPassword $securePass `
        -Path $_.OU `
        -Enabled $true `
        -ChangePasswordAtLogon $true
}

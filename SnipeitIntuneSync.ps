

$SnipeitToken = Get-AutomationVariable -Name 'SnipeitToken'
$SnipeitURL = Get-AutomationVariable -Name 'SnipeitURL'

Connect-SnipeitPS `
		-apiKey $SnipeitToken `
		-url $SnipeitURL

#https://oofhours.com/2019/11/29/app-based-authentication-with-intune/
$tenant = Get-AutomationVariable -Name 'tenant'
$authority = “https://login.windows.net/$tenant”
$clientId = Get-AutomationVariable -Name 'clientId'
$clientSecret = Get-AutomationVariable -Name 'clientSecret'

Update-MSGraphEnvironment -AppId $clientId -Quiet
Update-MSGraphEnvironment -AuthUrl $authority -Quiet
Connect-MSGraph -ClientSecret $ClientSecret -Quiet



#Get all Assets
[System.Collections.ArrayList]$IntuneAssets = Get-IntuneManagedDevice | Get-MSGraphAllPages | Where { $_.serialNumber -ne 0 }
$SnipeitAssets = Get-SnipeitAsset -all
$SnipeitModels= Get-SnipeitModel -all
$SnipeitManufacturers= Get-SnipeitManufacturer -all 
$SnipeitUsers = Get-SnipeitUser -all
$SnipeitCategories = Get-SnipeitCategory -all

#Found double Serial Numbers
[System.Collections.ArrayList]$DoubleSerialNr = @()
foreach ($IntuneAsset in $IntuneAssets) {
    $Counter = 0
    foreach ($IntuneAsset2 in $IntuneAssets) {
        if( $IntuneAsset.serialNumber.Equals($IntuneAsset2.serialNumber) ) {$Counter++}
    }
    if( $Counter -gt 1 -and $DoubleSerialNr -notcontains $IntuneAsset.serialNumber) {
        $IndexinArray = $DoubleSerialNr.Add($IntuneAsset.serialNumber)
        Write-Output "Found multiple Serial Numbers for : " $IntuneAsset.serialNumber
    }
}

#Delete double Serial Numbers. Keep newest Serial Number
foreach ($SerialNr in $DoubleSerialNr) {
    $IntuneAssetsindex = 0

    $collectionWithItems = New-Object System.Collections.ArrayList

    $BiggestEnrollmentDateTime = (get-date 2000-01-01)
    $IndexofBiggestEnrollmentDateTime = -1

    foreach ($IntuneAsset in $IntuneAssets) {
        $IntuneAssetsindex++
        if( $IntuneAsset.serialNumber.Equals($SerialNr) ) {
            
            #Write-Host "Index: " $IntuneAssetsindex " Serial: " $IntuneAsset.serialNumber
            #Write-Host "Compare " $BiggestEnrollmentDateTime " with " $IntuneAsset.enrolledDateTime
            if( $IntuneAsset.enrolledDateTime -gt $BiggestEnrollmentDateTime){
                #Write-Host "New LatestDate: " $IntuneAsset.enrolledDateTime
                $BiggestEnrollmentDateTime = $IntuneAsset.enrolledDateTime
                if($IndexofBiggestEnrollmentDateTime -eq -1){
                    $IndexofBiggestEnrollmentDateTime = $IntuneAssetsindex
                }else{
                    $tempindexof = $collectionWithItems.Add($IndexofBiggestEnrollmentDateTime)
                    $IndexofBiggestEnrollmentDateTime = $IntuneAssetsindex
                }
            }else{
                 $tempindexof = $collectionWithItems.Add($IntuneAssetsindex)
            }
        }
    }
    #Write-Host "BiggestEnrollmentDateTime: " $BiggestEnrollmentDateTime "with index: " $IndexofBiggestEnrollmentDateTime
    #Write-Host "Delete Values with Index: " $collectionWithItems

    foreach ($Valuetodelete in $collectionWithItems) {
        $IntuneAssets.RemoveAt($Valuetodelete - 1)
    }
}

foreach ($IntuneAsset in $IntuneAssets) {
    $FoundinSnipeit = 0
    $SnipeitAssetID    = 0
    foreach ($SnipeitAsset in $SnipeitAssets) {
        if( $IntuneAsset.serialNumber.Equals($SnipeitAsset.serial) ){
            $FoundinSnipeit = 1
            $SnipeitAssetID = $SnipeitAsset.id
        }
    }
    if($FoundinSnipeit -eq 1){
        #Write-Host "Found Asset: " $IntuneAsset.serialNumber " in Snipeit"
    }
    else{
        #Write-Host "New Asset for Snipeit: " $IntuneAsset.serialNumber
    }
        #Is Manufacturer in Snipeit ?
        $FoundSnipeitManufacturer = 0
        $SnipeitManufacturerID    = 0
        if ($IntuneAsset.manufacturer.Equals("") -or $IntuneAsset.manufacturer.Equals(" ") -or $IntuneAsset.manufacturer.Equals("---")){
            Write-Output "Manufacturer name not valide. Use Unknown as Manufacturer"
            $IntuneAsset.manufacturer = "Unknown"
        }
        foreach ($SnipeitManufacturer in $SnipeitManufacturers) {
            if( $IntuneAsset.manufacturer.Equals($SnipeitManufacturer.name) ){
                $FoundSnipeitManufacturer = 1
                $SnipeitManufacturerID = $SnipeitManufacturer.id
            }
        }
        if( $FoundSnipeitManufacturer -eq 1){
            #Write-Host "Manufacturer found in Snipeit"
        }else{
            Write-Output "New Manufacturer for Snipeit: " $IntuneAsset.manufacturer
            New-SnipeitManufacturer -Name $IntuneAsset.manufacturer
            
            #Refresh Manufacturer List and get Manufacturer id 
            $SnipeitManufacturers= Get-SnipeitManufacturer -all
            foreach ($SnipeitManufacturer in $SnipeitManufacturers) {
                if( $IntuneAsset.manufacturer.Equals($SnipeitManufacturer.name) ){
                    $SnipeitManufacturerID = $SnipeitManufacturer.id
                }
            }
        }
        
        #Is deviceCategory in Snipeit ?
        $FoundSnipeitCategory = 0
        $SnipeitCategoryID    = 0
        foreach ($SnipeitCategory in $SnipeitCategories) {
            if( $IntuneAsset.deviceCategoryDisplayName.Equals($SnipeitCategory.name) ){
                $FoundSnipeitCategory = 1
                $SnipeitCategoryID = $SnipeitCategory.id
            }
        }
        if( $FoundSnipeitCategory -eq 1){
            #Write-Host "Category found in Snipeit"
        }else{
            Write-Output "New Category for Snipeit: " $IntuneAsset.deviceCategoryDisplayName
            New-SnipeitCategory -Name $IntuneAsset.deviceCategoryDisplayName -category_type asset 
            
            #Refresh deviceCategory List and get Category id
            $SnipeitCategories = Get-SnipeitCategory -all
            foreach ($SnipeitCategory in $SnipeitCategories) {
                if( $IntuneAsset.deviceCategoryDisplayName.Equals($SnipeitCategory.name) ){
                    $SnipeitCategoryID = $SnipeitCategory.id
                }
            }
        }
        
        #Is Model in Snipeit ?
        $FoundSnipeitModel = 0
        $SnipeitModelID    = 0
        if ($IntuneAsset.model.Equals("") -or $IntuneAsset.model.Equals(" ") -or $IntuneAsset.model.Equals("---")){
            Write-Output "Model not valide. Use Unknown as Model"
            $IntuneAsset.model = "Unknown"
        }
        foreach ($SnipeitModel in $SnipeitModels) {
            if( $IntuneAsset.model.Equals($SnipeitModel.model_number) ){
                $FoundSnipeitModel = 1
                $SnipeitModelID = $SnipeitModel.id
            }
        }
        if( $FoundSnipeitModel -eq 1){
            #Write-Host "Model found in Snipeit"
        }else{
            Write-Output "New Model for Snipeit: " $IntuneAsset.model
            New-SnipeitModel -Name $IntuneAsset.model -category_id $SnipeitCategoryID -manufacturer_id $SnipeitManufacturerID -model_number $IntuneAsset.model
            #Refresh Manufacturer List
            $SnipeitModels= Get-SnipeitModel -all
            foreach ($SnipeitModel in $SnipeitModels) {
                if( $IntuneAsset.model.Equals($SnipeitModel.model_number) ){
                    $SnipeitModelID = $SnipeitModel.id
                }
            }
        }

        #Find Person to Asset
        $FoundSnipeitPerson = 0
        $SnipeitPersonID    = 0
        if ($IntuneAsset.userPrincipalName.Equals("") -or $IntuneAsset.userPrincipalName.Equals(" ") -or $IntuneAsset.userPrincipalName.Equals("---")){
            Write-Output "userPrincipalName not valide. Use Unknown as userPrincipalName"
            $IntuneAsset.userPrincipalName = "unknow@person.com"
			$SnipeitPersonID = 164
        }
        foreach ($SnipeitUser in $SnipeitUsers) {
            if( $IntuneAsset.userPrincipalName.Equals($SnipeitUser.email) ){
                $FoundSnipeitPerson = 1
                $SnipeitPersonID = $SnipeitUser.id
            }
        }
        if( $FoundSnipeitPerson -eq 1){
            #Write-Host "Person found in Snipeit"
        }else{
            Write-Output "New Person for Snipeit : " $IntuneAsset.userPrincipalName " . But add no new user"
            $SnipeitPersonID = 164
        }
        
        if($FoundinSnipeit -eq 1){
            #Asset exist in Snipeit. Check for Updates
            
            $UpdateAssetinSnipeit = 0
            foreach ($SnipeitAsset in $SnipeitAssets) {
                if( $SnipeitAsset.id -eq $SnipeitAssetID ){
                    if($SnipeitAsset.assigned_to.id -ne $SnipeitPersonID){
                        $UpdateAssetinSnipeit = 1
                    }
                    if(-not ($SnipeitAsset.asset_tag.Equals($IntuneAsset.serialNumber))){
                        $UpdateAssetinSnipeit = 1
                    }
                    if(-not ($SnipeitAsset.name.Equals($IntuneAsset.deviceName))){
                        $UpdateAssetinSnipeit = 1
                    }
                }
            }

            if($UpdateAssetinSnipeit -eq 1){
                Write-Output "Update Asset with SerialNr.: " $IntuneAsset.serialNumber
                #Write-Host "-id " $SnipeitAssetID " -assigned_to " $SnipeitPersonID " -asset_tag " $IntuneAsset.serialNumber  " -name " $IntuneAsset.deviceName
                Set-SnipeitAsset -id $SnipeitAssetID -assigned_to $SnipeitPersonID -asset_tag $IntuneAsset.serialNumber -name $IntuneAsset.deviceName -Confirm:$false
            }else{
                #Write-Output "No update necessary for Asset with SerialNr.: " $IntuneAsset.serialNumber
            }

       
        }
        else{
            #New Asset for Snipeit. Add new Asset to Snipeit
			Write-Output "New Asset with SerialNr.: " $IntuneAsset.serialNumber
            New-SnipeitAsset -status_id 2 -model_id $SnipeitModelID -name $IntuneAsset.deviceName -asset_tag $IntuneAsset.serialNumber -serial $IntuneAsset.serialNumber -assigned_id $SnipeitPersonID -checkout_to_type user -Confirm:$false
            #New-SnipeitAsset -status_id 2 -model_id $SnipeitModelID -name $IntuneAsset.deviceName -asset_tag $IntuneAsset.serialNumber -serial $IntuneAsset.serialNumber -assigned_id 0 -checkout_to_type user
        }
}

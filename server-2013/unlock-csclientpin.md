﻿---
title: Unlock-CsClientPin
TOCTitle: Unlock-CsClientPin
ms:assetid: eef7877c-0302-4ce7-84f5-06968d0623b9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412982(v=OCS.15)
ms:contentKeyID: 48277114
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Unlock-CsClientPin

 

_**Última modificación del tema:** 2015-03-09_

Enables an administrator to unlock the personal identification number (PIN) for a specified user. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    Unlock-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

In Example 1, the **Unlock-CsClientPin** cmdlet is used to unlock the PIN belonging to the user litwareinc\\kenmyer.

    Unlock-CsClientPin -Identity "litwareinc\kenmyer"

## EXAMPLE 2

In Example 2, the **Unlock-CsClientPin** cmdlet is used to unlock all the PINs that are currently locked. To do this, the **Get-CsUser** cmdlet is first used to return a collection of all the users who have been enabled for Lync Server. That collection is then piped to the **Get-CsClientPinInfo** cmdlet, which is used in conjunction with the **Where-Object** cmdlet to select only those users where the IsLockedOut property is equal to (-eq) to True ($True).

The resulting filtered collection is then piped to the **Unlock-CsClientPin** cmdlet, which unlocks the PIN for each user whose PIN was previously locked.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsLockedOut -eq $True} | Unlock-CsClientPin 

## Detailed Description

Lync Server enables users to connect to the system or to join public switched telephone network (PSTN) conferences by using a telephone. Typically, logging on to the system or joining a conference requires the user to enter a user name or password. However, entering a user name and password can be a problem if you are using a phone that does not have an alphanumeric keypad. Because of that, Lync Server enables you to supply users with numeric-only PINs; when prompted, users can then log on to the system or join a conference by entering the PIN instead of a user name and password.

This is true, however, only if the user's PIN is unlocked. If a PIN has been locked (either because the user repeatedly failed to log on or because an administrator explicitly locked the PIN), the user will not be able to access the system or join a conference by using PIN authentication. (However, that user will still be able to use an application such as Lync to log on to the system by supplying a user name and password.) If a PIN has been locked, there is only one way to restore the user's ability to access the system by using PIN authentication: the locked PIN must be unlocked by an administrator. This can be done by using the **Unlock-CsClientPin** cmdlet.

Note that, by default, the firewall exceptions for SQL Server Express are not enabled when you install the Standard Edition of Lync Server. That means that you will not be able to run the **Unlock-CsClientPin** cmdlet from a remote instance of Windows PowerShell; that’s because your command will not be able to traverse the firewall and access the SQL Server Express database. (However, you can still run the cmdlet locally on the Standard Edition server itself.) To run the **Unlock-CsClientPin** cmdlet remotely against a Standard Edition server you will need to manually enable the firewall exceptions for SQL Server Express.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Unlock-CsClientPin** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Unlock-CsClientPin"}

## Parámetros


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Required</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Required</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identity of the user account for which the PIN should be unlocked. User Identities can be specified by using one of four formats: 1) the user's SIP address; 2) the user's user principal name (UPN); 3) the user's domain name and logon name, in the form domain\logon (for example, litwareinc\kenmyer); and, 4) the user's Active Directory display name (for example, Ken Myer). User Identities can also be referenced by using the user’s Active Directory distinguished name.</p>
<p>In addition, you can use the asterisk (*) wildcard character when using the Display Name as the user Identity. For example, the Identity &quot;* Smith&quot; returns all the users who have a display name that ends with the string value &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses the display of any non-fatal error message that might occur when running the command.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Input Types

String value or Microsoft.Rtc.Management.ADConnect.Schema.ADUser object. The **Unlock-CsClientPin** cmdlet accepts pipelined input of string values representing the Identity of a user account. The cmdlet also accepts pipelined input of user objects.

## Return Types

The **Unlock-CsClientPin** cmdlet does not return a value or object. Instead, the cmdlet configures one or more instances of the Microsoft.Rtc.Management.UserPinService.PinInfoDetails object.

## Vea también

#### Otros recursos

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Lock-CsClientPin](lock-csclientpin.md)  
[Set-CsClientPin](set-csclientpin.md)


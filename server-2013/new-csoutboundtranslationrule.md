﻿---
title: New-CsOutboundTranslationRule
TOCTitle: New-CsOutboundTranslationRule
ms:assetid: aa6011e5-c48d-4fcc-ba65-bdec341234ed
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg412803(v=OCS.15)
ms:contentKeyID: 48276310
ms.date: 01/07/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsOutboundTranslationRule

 

_**Última modificación del tema:** 2015-03-09_

Creates a new outbound translation rule. An outbound translation rule converts phone numbers to the local dialing format for interaction with private branch exchange (PBX) systems. Este cmdlet se presentó en Lync Server 2010.

## Sintaxis

    New-CsOutboundTranslationRule -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsOutboundTranslationRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

This example creates a new outbound translation rule for site Redmond named Prefix Redmond. Because no other parameters are specified, the rule is created with the default values. Notice that the value passed to the Identity parameter is in double-quotes; this is because the name of the rule (Prefix Redmond) contains a space. If the rule name does not contain a space you don’t need to enclose the Identity in double quotes.

    New-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond"

## EXAMPLE 2

This example creates a new global outbound translation rule named SeattleSevenDigit. (Note: Rather than specifying a Parent and a Name, we could have instead created this same rule by specifying -Identity global/SeattleSevenDigit.) We’ve included a Description explaining that this rule is for translating numbers in E.164 format to a seven-digit format. In addition, Pattern and Translation values have been specified. These values translate an E.164 number (in this case 12 digits beginning with +1425), specified by the regular expression in the Pattern, to a seven-digit number by removing the first five digits. For example, the number +14255551212 would be translated to the number 5551212.

    New-CsOutboundTranslationRule -Parent global -Name SeattleSevenDigit -Description "Convert to seven digits" -Pattern '^\+1425(\d{7})$' -Translation '$1'

## Detailed Description

Call this cmdlet to create a new outbound translation rule. Lync Server normalizes phone numbers to E.164 format. However, many private branch exchange (PBX) systems aren’t able to work with this format. Outbound translations rules translate the number to the local dialing format prior to sending the number to the Servidor de mediación or gateway.

Each outbound translation rule is associated with a trunk configuration. More than one outbound translation rule can be associated with each configuration. Therefore, the Identity for each rule consists of a scope along with a name that is unique within the scope (in the format scope/name, for example site:Redmond/OBR1). The rule is automatically associated with the trunk configuration with the same scope. If you call the **New-CsOutboundTranslationRule** cmdlet and specify a scope at which a trunk configuration has not yet been defined, the trunk configuration will be created with the given scope, the outbound translation rule, and default values.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **New-CsOutboundTranslationRule** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsOutboundTranslationRule"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>A unique identifier for the outbound translation rule. The Identity includes the scope at which the rule is applied and the name of the rule, and must be at the global, site, or service (PSTNGateway only) scope. For example, site:Redmond/OutboundRule1 and PstnGateway:Redmond.litwareinc.com/OutboundRule2.</p>
<p>If the Identity parameter is specified, you cannot specify values for the Name or Parent parameters.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>The name of the outbound translation rule. If no Name is supplied, an Identity consisting of a scope and name must be specified. If a Name is supplied, the Parent parameter is also required, but an Identity cannot be specified.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>The scope of the outbound translation rule. If a value is specified for this parameter, a value must also be specified for the Name parameter. However, the Identity parameter cannot be specified. If the Parent and Name parameters aren’t specified, the Identity must be.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se le pedirá confirmación antes de ejecutar el comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>A description of the outbound translation rule. This description will help identify the purpose of the rule.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea una referencia de objeto sin confirmar realmente el objeto como cambio permanente. Si se asigna la salida de este cmdlet llamado con este parámetro en una variable, puede realizar cambios en las propiedades de la referencia del objeto y después confirmar estos cambios, llamando a este conjunto coincidente de cmdlet, - cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>A regular expression representing the number pattern to which the Translation will be applied.</p>
<p>Default: ^\+(\d*)$</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Int32</p></td>
<td><p>If a number matches the Pattern of more than one outbound translation rule, rules are applied in priority order. Use this parameter to assign a priority to the rule.</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>A regular expression that will be applied to the number matching the Pattern to prepare that number for outbound routing.</p>
<p>Default: $1</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describe qué sucedería si se ejecutara el comando sin ejecutarlo realmente.</p></td>
</tr>
</tbody>
</table>


## Input Types

None.

## Return Types

This cmdlet creates an object of type Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule.

## Vea también

#### Otros recursos

[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)


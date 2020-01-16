---
title: PKEY\_AudioDevice\_NeverSetAsDefaultEndpoint
description: PKEY\_AudioDevice\_NeverSetAsDefaultEndpoint
ms.assetid: cb619972-d9d9-4f33-bb4a-720bfc29e3e8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ebed7e76f697f3d42ea7291595fae9108162b23
ms.sourcegitcommit: 1addd14b2063aba321f5428a23393f22f59c02b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2020
ms.locfileid: "76035720"
---
# <a name="pkey_audiodevice_neversetasdefaultendpoint"></a>PKEY\_AudioDevice\_NeverSetAsDefaultEndpoint


既定のデバイスとして選択されないように、特定のデバイスを設定することもできます。 これには、モデムラインや医療オーディオデバイスなどが含まれます。Windows 7 以降のバージョンの Windows では、 **PKEY\_audiodevice\_NeverSetAsDefaultEndpoint**レジストリキーを使用して、デバイスのエンドポイントを既定のエンドポイントとして選択できないようにしています。

次の INF ファイルの抜粋では、 **PKEY\_AudioDevice\_NeverSetAsDefaultEndpoint**を使用して、既定として選択されないようにエンドポイントを設定する方法を示しています。

```inf
[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid= {4d36e96c-e325-11ce-bfc1-08002be10318}
...

[USBAudio]
...

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,"GLOBAL",USBAudio.Interface
...

[USBAudio.Interface]
AddReg=Xyz.AddReg
...

;; AddReg section to setup endpoint so that
;; it cannot be selected as the default endpoint.
[Xyz.AddReg]
HKR,"EP\\n",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_GUID%
HKR,"EP\\n",%PKEY_AudioDevice_NeverSetAsDefaultEndpoint%,0x00010001,NeverSetAsDefaultEndpointMaskValue
...

[Strings]
KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_NeverSetAsDefaultEndpoint = "{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},3"
...
```

前の例では、NeverSetAsDefaultEndpointMaskValue は、デバイスロールフラグとデータフローフラグの組み合わせである DWORD マスク値を表します。

次の INF ファイルスニペットは、デバイスロールとデータフロー方向に関係なく、そのエンドポイントが既定値として選択されないように、未定義の出力デバイス (KSNODETYPE\_OUTPUT\_UNDEFINED) を設定する方法を示しています。

```inf
[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid= {4d36e96c-e325-11ce-bfc1-08002be10318}
...

[USBAudio]
...

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,"GLOBAL",USBAudio.Interface
...

[USBAudio.Interface]
AddReg=MDVAD.EPProperties.AddReg
...

;; AddReg section to setup endpoint so that
;; it cannot be selected as the default endpoint.
[MDVAD.EPProperties.AddReg]
HKR,"EP\\0",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_OUTPUT_UNDEFINED%
HKR,"EP\\0",%PKEY_AudioDevice_NeverSetAsDefaultEndpoint%,0x00010001,0x00000305
...

[Strings]
KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
KSNODETYPE_OUTPUT_UNDEFINED="{DFF21CE0-F70F-11D0-B917-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_NeverSetAsDefaultEndpoint = "{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},3"
```

前の例では、0x00000305 は、 **PKEY\_AudioDevice\_NeverSetAsDefaultEndpoint**で使用可能なすべてのフラグとマスクのビットごとの or の組み合わせです。 次の表に、フラグとマスク、およびそれらの値を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグまたはエンドポイントマスク</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FLOW_MASK_CAPTURE</p></td>
<td align="left"><p>0x00000200</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLOW_MASK_RENDER</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ROLE_MASK_COMMUNICATION</p></td>
<td align="left"><p>0x00000004</p></td>
</tr>
<tr class="even">
<td align="left"><p>ROLE_MASK_CONSOLE</p></td>
<td align="left"><p>0x00000001</p></td>
</tr>
</tbody>
</table>

 

 

 






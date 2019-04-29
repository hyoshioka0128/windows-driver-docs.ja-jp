---
title: 鍵\_AudioDevice\_NeverSetAsDefaultEndpoint
description: 鍵\_AudioDevice\_NeverSetAsDefaultEndpoint
ms.assetid: cb619972-d9d9-4f33-bb4a-720bfc29e3e8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25dcdea96e8c08e213814d6b505b268eccd65864
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332214"
---
# <a name="pkeyaudiodeviceneversetasdefaultendpoint"></a>鍵\_AudioDevice\_NeverSetAsDefaultEndpoint


既定のデバイスとしてことはありません選択できるように、特定のデバイスを設定することがあります。 これらは、たとえば、モデムの線と医療のオーディオ デバイスあります。Windows 7 および Windows の以降のバージョンの提供、**鍵\_AudioDevice\_NeverSetAsDefaultEndpoint**のため、既定のエンドポイントとして、デバイスのエンドポイントを選択できるようにレジストリ キー。

次の INF ファイルの抜粋は、使用する方法を示します**鍵\_AudioDevice\_NeverSetAsDefaultEndpoint**既定として選択することがないように、エンドポイントを設定します。

```inf
[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid= {4d36e96c-e325-11ce-bfc1-08002be10318}
...

[USBAudio]
...

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,”GLOBAL”,USBAudio.Interface
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
KSCATEGORY_AUDIO=” {6994AD04-93EF-11D0-A3CC-00A0C9223196}”
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_NeverSetAsDefaultEndpoint = "{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},3"
...
```

前の例では、NeverSetAsDefaultEndpointMaskValue は、デバイスの役割のフラグとデータ フローのフラグの組み合わせである DWORD マスク値を表します。

次の INF ファイルのスニペットは、未定義の出力デバイスかを示します (KSNODETYPE\_出力\_UNDEFINED) デバイスの役割とデータ フローの方向に関係なく、既定値としてそのエンドポイントが選択されているしないように設定します。

```inf
[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid= {4d36e96c-e325-11ce-bfc1-08002be10318}
...

[USBAudio]
...

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,”GLOBAL”,USBAudio.Interface
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
KSCATEGORY_AUDIO=” {6994AD04-93EF-11D0-A3CC-00A0C9223196}”
KSNODETYPE_OUTPUT_UNDEFINED="{DFF21CE0-F70F-11D0-B917-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_NeverSetAsDefaultEndpoint = "{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},3"
```

前の例では、0x00000305 はのすべてのフラグとマスクの使用可能なビットごとの OR の組み合わせ**鍵\_AudioDevice\_NeverSetAsDefaultEndpoint**します。 次の表は、フラグ、およびマスクとその値を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグまたはエンドポイントのマスク</th>
<th align="left">値</th>
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

 

 

 






---
title: PKEY\_AudioDevice\_EnableEndpointByDefault デフォルト)
description: PKEY\_AudioDevice\_EnableEndpointByDefault デフォルト)
ms.assetid: bde2c06d-9418-4f6d-960a-0ebec83bf397
ms.date: 01/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 27218a0a235286887158f16e273132fc6b1a6826
ms.sourcegitcommit: 1addd14b2063aba321f5428a23393f22f59c02b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2020
ms.locfileid: "76035724"
---
# <a name="pkey_audiodevice_enableendpointbydefault"></a>PKEY\_AudioDevice\_EnableEndpointByDefault デフォルト)

Windows 7 以降のバージョンの Windows では、エンドポイントビルダーによってエンドポイントがフォームファクターに分類されます。 これらのフォームファクターは、エンドポイントが接続されているカーネルストリーミング (KS) フィルターのピンの KSNODETYPE GUID に基づいています。 オーディオエンドポイントビルダーが特定のエンドポイント (たとえば、UnknownFormFactor などのフォームファクター型を持つエンドポイント) を列挙すると、エンドポイントビルダーはこれらのエンドポイントを無効および非表示として作成します。 そのため、使用する前に、コントロールパネルの [サウンド] プログラムを使用して、そのようなエンドポイントを有効にする必要があります。

エンドポイントが既定で有効または無効として作成されるようにこの動作をオーバーライドする場合、Windows 7 では、 **PKEY\_AudioDevice\_EnableEndpointByDefault**レジストリキーを使用してこれを行うことができます。

エンドポイントビルダーは、次のいずれかの KSNODETYPE 値を無効および非表示にしてエンドポイントを作成します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KS ノードの種類</th>
<th align="left">フォーム ファクター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSCATEGORY_AUDIO</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_BIDIRECTIONAL_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_EMBEDDED_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_EQUALIZATION_NOISE</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_EXTERNAL_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_INPUT_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_LEVEL_CALIBRATION_NOISE_SOURCE</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_OUTPUT_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_TELEPHONY_UNDEFINED</p></td>
<td align="left"><p>UnknownFormFactor</p></td>
</tr>
</tbody>
</table>

Windows 7 以降のバージョンの Windows では、LineLevel というフォームファクターのエンドポイントがありますが、KSNODETYPE が KSNODETYPE\_LINE\_コネクタの場合は、"無効" と "非表示" として作成されます。 次のエンドポイントがこのカテゴリに分類されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KS ノードの種類</th>
<th align="left">フォーム ファクター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSNODETYPE_1394_DA_STREAM</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_1394_DV_STREAM_SOUNDTRACK</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_ANALOG_TAPE</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_CABLE_TUNER_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_CD_PLAYER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_DAT_IO_DIGITAL_AUDIO_TAPE</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_DCC_IO_DIGITAL_COMPACT_CASSETTE</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_DSS_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_DVD_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_LEGACY_AUDIO_CONNECTOR</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_MINIDISK</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_MULTITRACK_RECORDER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_PHONOGRAPH</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_RADIO_RECEIVER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_RADIO_TRANSMITTER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_SATELLITE_RECEIVER_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_SYNTHESIZER</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_TV_TUNER_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_VCR_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_VIDEO_DISC_AUDIO</p></td>
<td align="left"><p>LineLevel</p></td>
</tr>
</tbody>
</table>

次の INF ファイルスニペットは、既定でエンドポイントを有効または無効にするために、 **PKEY\_AudioDevice\_EnableEndpointByDefault**を使用する方法を示しています。

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

;; AddReg section to set default behavior of endpoint
[Xyz.AddReg]
HKR,"EP\\n",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_GUID%
HKR,"EP\\n",%PKEY_AudioDevice_EnableEndpointByDefault%,0x00010001,EnableEndpointByDefaultMaskValue
...

[Strings]
KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_EnableEndpointByDefault="{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},4"
...
```

前の例では、EnableEndpointByDefaultMaskValue は、enable または disable フラグ (フラグ\_ENABLE または FLAG\_DISABLE) とデータフローフラグ (フロー\_マスク\_レンダーまたはフロー\_マスク\_キャプチャ) の組み合わせである DWORD マスク値を表します。

次の INF ファイルスニペットは、CD プレーヤーが既定で有効になり、入力デバイスとして構成されるように設定されている (フロー\_マスク\_キャプチャ) 方法を示しています。

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

;; AddReg section is used to set default behavior of endpoint for CD player.
;; Enable by default for KSNODETYPE_CD_PLAYER
[MDVAD.EPProperties.AddReg]
HKR,"EP\\0",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_CD_PLAYER%
HKR,"EP\\0",%PKEY_AudioDevice_EnableEndpointByDefault%,0x00010001,0x00000201
...

[Strings]
KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
KSNODETYPE_CD_PLAYER="{DFF220E3-F70F-11D0-B917-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_EnableEndpointByDefault="{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},4"
…
```

前の例では、フロー\_マスクのビットごとの or の組み合わせ\_CAPTURE と FLAG\_ENABLE は、0x00000200 と0x00000001 のビットごとの or の組み合わせが、0x00000201 の結果と同じになります。 次の表に、 **PKEY\_AudioDevice\_EnableEndpointByDefault**使用できるフラグとマスクの値を示します。

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
<td align="left"><p>FLAG_DISABLE</p></td>
<td align="left"><p>0x00000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLAG_ENABLE</p></td>
<td align="left"><p>0x00000001</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLOW_MASK_CAPTURE</p></td>
<td align="left"><p>0x00000200</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLOW_MASK_RENDER</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
</tbody>
</table>

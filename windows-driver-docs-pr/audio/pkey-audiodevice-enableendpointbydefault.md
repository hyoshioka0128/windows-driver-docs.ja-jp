---
title: 鍵\_AudioDevice\_EnableEndpointByDefault
description: 鍵\_AudioDevice\_EnableEndpointByDefault
ms.assetid: bde2c06d-9418-4f6d-960a-0ebec83bf397
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35db8b33a882f7a61ddc7046dc1ee1971a0fe769
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332218"
---
# <a name="pkeyaudiodeviceenableendpointbydefault"></a>鍵\_AudioDevice\_EnableEndpointByDefault


Windows 7 および Windows の以降のバージョンでは、エンドポイント ビルダーは、フォーム ファクターにエンドポイントを分類します。 これらのフォーム ファクターは、ストリーミング エンドポイントが接続されている (KS) フィルター、カーネルで pin の KSNODETYPE GUID に基づいています。 オーディオ エンドポイント ビルダー UnknownFormFactor などのフォーム ファクター型など、特定のエンドポイントを列挙するときに、エンドポイント ビルダーは、無効になっており、非表示としてこれらのエンドポイントを作成します。 これを使用するには、このようなエンドポイントを有効にする、コントロール パネルのサウンドのプログラムを使用する必要があります。

有効になっていると、エンドポイントが作成されるように、この動作をオーバーライドする場合や、既定では、Windows 7 で無効化を提供、**鍵\_AudioDevice\_EnableEndpointByDefault**できるレジストリ キーそのためにします。

エンドポイント ビルダーは、無効になっており、非表示として KSNODETYPE 値は次のいずれかのエンドポイントを作成します。

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

 

Windows 7 および Windows の以降のバージョンでは、エンドポイント ソースコードリスティングのフォーム ファクターではなく、KSNODETYPE、等しくない KSNODETYPE\_行\_コネクタも無効になっているとして作成され、非表示になります。 次のエンドポイントは、このカテゴリに分類されます。

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
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_1394_DV_STREAM_SOUNDTRACK</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_ANALOG_TAPE</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_CABLE_TUNER_AUDIO</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_CD_PLAYER</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_DAT_IO_DIGITAL_AUDIO_TAPE</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_DCC_IO_DIGITAL_COMPACT_CASSETTE</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_DSS_AUDIO</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_DVD_AUDIO</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_LEGACY_AUDIO_CONNECTOR</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_MINIDISK</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_MULTITRACK_RECORDER</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_PHONOGRAPH</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_RADIO_RECEIVER</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_RADIO_TRANSMITTER</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_SATELLITE_RECEIVER_AUDIO</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_SYNTHESIZER</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_TV_TUNER_AUDIO</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_VCR_AUDIO</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_VIDEO_DISC_AUDIO</p></td>
<td align="left"><p>ソースコードリスティング</p></td>
</tr>
</tbody>
</table>

 

次の INF ファイルのスニペットは、使用する方法を示します**鍵\_AudioDevice\_EnableEndpointByDefault**を有効または、既定では、エンドポイントを無効にします。

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

;; AddReg section to set default behavior of endpoint
[Xyz.AddReg]
HKR,"EP\\n",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_GUID%
HKR,"EP\\n",%PKEY_AudioDevice_EnableEndpointByDefault%,0x00010001,EnableEndpointByDefaultMaskValue
...

[Strings]
KSCATEGORY_AUDIO=” {6994AD04-93EF-11D0-A3CC-00A0C9223196}”
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_EnableEndpointByDefault="{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},4”
...
```

前の例では、EnableEndpointByDefaultMaskValue が有効化または無効にするフラグの組み合わせである DWORD マスクの値を表します (フラグ\_フラグを有効または\_を無効にする) とフラグのフロー データ (フロー\_マスク\_レンダリングまたはフロー\_マスク\_キャプチャ) します。

CD プレーヤーのセットアップ方法ように既定で有効にし、入力デバイスとして構成されて次の INF ファイルのスニペットを示しています (フロー\_マスク\_キャプチャ) します。

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

;; AddReg section is used to set default behavior of endpoint for CD player.
;; Enable by default for KSNODETYPE_CD_PLAYER 
[MDVAD.EPProperties.AddReg]
HKR,"EP\\0",%PKEY_AudioEndpoint_Association%,,%KSNODETYPE_CD_PLAYER%
HKR,"EP\\0",%PKEY_AudioDevice_EnableEndpointByDefault%,0x00010001,0x00000201
...

[Strings]
KSCATEGORY_AUDIO=” {6994AD04-93EF-11D0-A3CC-00A0C9223196}”
KSNODETYPE_CD_PLAYER="{DFF220E3-F70F-11D0-B917-00A0C9223196}"
PKEY_AudioEndpoint_Association="{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioDevice_EnableEndpointByDefault="{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},4”
…
```

前の例では、フローのビットごとの OR の組み合わせで\_マスク\_キャプチャとフラグ\_有効にするには、ビットごとの OR の組み合わせ 0x00000200 と 0x00000001 0x00000201 の結果でに相当します。 次の表は、値のフラグとマスクで使用できる**鍵\_AudioDevice\_EnableEndpointByDefault**します。

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

 

 

 






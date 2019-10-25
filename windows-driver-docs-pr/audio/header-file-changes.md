---
title: ヘッダー ファイルの変更
description: ヘッダー ファイルの変更
ms.assetid: 9212aa8d-bb11-4ade-a70c-274a7ffe83ef
keywords:
- データ形式 WDK オーディオ
- WDK オーディオ、データをフォーマットします
- WDK のオーディオデータ形式
- WDK オーディオ、マルチチャネルをフォーマットします。
- マルチチャネル形式 WDK オーディオ
- ホームシアターシステム WDK オーディオ
- スピーカー WDK オーディオ、ホーム-月、システム
- オーディオドライバー WDK、ホームシアターシステム
- WDM オーディオドライバー WDK、ホームシアターシステム
- 7.1 ホームシアタースピーカー WDK オーディオ
- 7.1 wide 構成スピーカー WDK オーディオ
- wide 構成スピーカー WDK オーディオ
- 5.1 サラウンドサウンドスピーカー WDK オーディオを挿入する
- サウンドスピーカーを囲む WDK オーディオ
- ヘッダーファイル WDK オーディオ
- Ksmedia.h
- Dsound
- チャネルマスク WDK オーディオ
- WDK オーディオを配置する
- WDM オーディオデータ形式 WDK
- データ形式 WDK オーディオ、ヘッダーファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cac6b949cb493e0b71e48c39f64a731aed130bb3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831196"
---
# <a name="header-file-changes"></a>ヘッダー ファイルの変更


Windows Driver Kit (WDK) には、Windows マルチメディアコントロールパネルでサポートされているスピーカー構成を定義する2つのヘッダーファイルが含まれています。

-   Ksmedia. h は、ksk[**プロパティ\_AUDIO\_channel\_config**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)プロパティ要求で使用される[**KSK AUDIO\_channel\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)構造体のチャネルマスクを定義します。

-   Dsound は、 **Idirectsound:: SetSpeakerConfig**メソッドに送信できるスピーカー構成識別子のリストを定義します。 このメソッドの詳細については、Windows SDK のドキュメントを参照してください。

Windows Server 2003、Windows XP SP1、Windows 2000、および Windows Me/98 では、次の表に示す5.1 および7.1 チャネルストリームのチャネルマスクが定義されています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター名</th>
<th align="left">チャネルマスク</th>
<th align="left">スピーカーの位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSAUDIO_SPEAKER_5POINT1</p></td>
<td align="left"><p>0x3F</p></td>
<td align="left"><p>FL、FR、FC、LFE、BL、BR</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSAUDIO_SPEAKER_7POINT1</p></td>
<td align="left"><p>0xFF</p></td>
<td align="left"><p>FL、FR、FC、LFE、BL、BR、FLC、FRC</p></td>
</tr>
</tbody>
</table>

 

前の表の2つのチャネルマスクは、5.1 スピーカー構成と7.1 スピーカー構成を表しています。 同じ2つのスピーカー構成を識別するために、Dsound は次のスピーカー構成 Id を定義します。

```cpp
  #define DSSPEAKER_5POINT1      0x00000006
  #define DSSPEAKER_7POINT1      0x00000007
```

Windows XP SP2 以降のバージョンの Windows では、Ksmedia. h は、5.1 と7.1 のチャネルのストリームについて、次の表に示すチャネルマスクを定義します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター名</th>
<th align="left">チャネルマスク</th>
<th align="left">スピーカーの位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSAUDIO_SPEAKER_5POINT1</p></td>
<td align="left"><p>0x3F</p></td>
<td align="left"><p>FL、FR、FC、LFE、BL、BR</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSAUDIO_SPEAKER_7POINT1_SURROUND</p></td>
<td align="left"><p>0x63F</p></td>
<td align="left"><p>FL、FR、FC、LFE、BL、BR、SL、SR</p></td>
</tr>
</tbody>
</table>

 

上記の2つのテーブルを比較することで、次の点が明らかになります。

-   2番目のテーブルでは、最初のテーブルのチャネルマスク0x3F の意味が変更されていません。ただし、Windows SP2 以降のバージョンの Windows では、KSK オーディオ\_スピーカー\_5POINT1 は、BL や BR ではなく、SL と SR のスピーカーを使用するように解釈されます。

-   値0x63F を持つ新しいチャネルマスクがサポートされています。 このチャンネルマスクは、7.1 ホームシアタースピーカー構成を表します。

-   **注**   windows Vista 以降のバージョンの windows では、ksk AUDIO\_スピーカー\_7POINT1 スピーカーの構成はサポートされなくなりました。 そのため、コントロールパネルでは使用できないオプションです。

     

同じスピーカー構成のセットを表すために、Dsound は次のスピーカー構成 Id を定義します。

```cpp
  #define DSSPEAKER_5POINT1             0x00000006
  #define DSSPEAKER_7POINT1             0x00000007
  #define DSSPEAKER_7POINT1_SURROUND    0x00000008
  #define DSSPEAKER_7POINT1_WIDE        DSSPEAKER_7POINT1
```

DSSPEAKER\_7POINT1\_サラウンドは、コントロールパネルの新しい7.1 ホームシアタースピーカー構成を表します。 DSSPEAKER\_7POINT1 と DSSPEAKER\_7POINT1\_WIDE は両方とも、同じ 7.1 wide configuration スピーカー構成の名前です。

DirectSound のスピーカー構成の詳細については、「 [Directsound スピーカー構成設定](directsound-speaker-configuration-settings.md)」を参照してください。

 

 





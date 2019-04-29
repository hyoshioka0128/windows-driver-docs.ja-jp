---
title: ヘッダー ファイルの変更
description: ヘッダー ファイルの変更
ms.assetid: 9212aa8d-bb11-4ade-a70c-274a7ffe83ef
keywords:
- データ形式の WDK オーディオ
- WDK のオーディオ、データを書式設定します。
- オーディオ データ形式 WDK
- WDK のオーディオ、マルチ チャネルを書式設定します。
- マルチ チャネルの形式の WDK オーディオ
- ホーム シアター システム WDK オーディオ
- スピーカーの WDK オーディオ、ホーム threater システム
- オーディオ ドライバー WDK、ホーム シアター システム
- WDM オーディオ ドライバー WDK、ホーム シアター システム
- ホーム シアターを 7.1 スピーカー WDK オーディオ
- 全体の構成を 7.1 スピーカー WDK オーディオ
- スピーカー WDK オーディオの全体の構成
- 5.1 サラウンド サウンド スピーカー WDK オーディオ
- サラウンド サウンド スピーカー WDK オーディオ
- ヘッダー ファイルの WDK オーディオ
- Ksmedia.h
- Dsound.h
- チャネル マスク WDK オーディオ
- WDK オーディオの位置
- オーディオ データ形式の WDM WDK
- データ形式の WDK オーディオ、ヘッダー ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e27ec98c27599f251f2c49062874110fd43b09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333549"
---
# <a name="header-file-changes"></a>ヘッダー ファイルの変更


Windows Driver Kit (WDK) には、Windows のマルチ メディアのコントロール パネルでサポートされているスピーカー構成を定義する 2 つのヘッダー ファイルが含まれています。

-   Ksmedia.h 定義のチャネル マスク、 [ **KSAUDIO\_チャネル\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537083)構造で使用される、 [ **KSPROPERTY\_オーディオ\_チャネル\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537250)プロパティ要求。

-   Dsound.h に送信できるスピーカー構成識別子のリストを定義する、 **IDirectSound::SetSpeakerConfig**メソッド。 この方法の詳細については、Windows SDK のドキュメントを参照してください。

Windows Server 2003、Windows XP SP1、Windows 2000、および Windows Me/98、Ksmedia.h 5.1 と 7.1 チャネル ストリームの次の表に示すチャネル マスクを定義します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター名</th>
<th align="left">チャネル マスク</th>
<th align="left">スピーカー位置</th>
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
<td align="left"><p>0 xff の場合</p></td>
<td align="left"><p>FL、FR、FC、LFE、BL、BR、FLC、FRC</p></td>
</tr>
</tbody>
</table>

 

上記の表に、2 つのチャネル マスクは、5.1 スピーカーの構成と 7.1 スピーカーの構成を表します。 同じ 2 つのスピーカー構成を特定するには、Dsound.h は、次のスピーカー構成 Id を定義します。

```cpp
  #define DSSPEAKER_5POINT1      0x00000006
  #define DSSPEAKER_7POINT1      0x00000007
```

Windows XP SP2、および以降のバージョンの Windows では、Ksmedia.h 5.1 と 7.1 チャネル ストリームの次の表に示すようにチャネル マスクを定義します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター名</th>
<th align="left">チャネル マスク</th>
<th align="left">スピーカー位置</th>
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

 

上記の 2 つのテーブルを比較すると、次の点が明らかに。

-   最初のテーブル内のチャネル マスク 0x3F の意味が変わらない 2 番目のテーブルであっても、Windows SP2 および以降のバージョンの Windows、KSAUDIO\_スピーカー\_BL および BR. ではなく SL と SR スピーカーを使用する 5POINT1 が解釈されます

-   0x63F の値を持つ新しいチャネル マスクがサポートされています。 このチャネル マスクは、ホーム シアターを 7.1 スピーカーの構成を表します。

-   **注**  で Windows Vista と以降のバージョンの Windows で、KSAUDIO\_スピーカー\_7POINT1 スピーカーの構成はサポートされていません。 その結果、コントロール パネルで、使用可能なオプションではありません。

     

スピーカーの構成の同じセットを表す、Dsound.h には次のスピーカー構成 Id を定義します。

```cpp
  #define DSSPEAKER_5POINT1             0x00000006
  #define DSSPEAKER_7POINT1             0x00000007
  #define DSSPEAKER_7POINT1_SURROUND    0x00000008
  #define DSSPEAKER_7POINT1_WIDE        DSSPEAKER_7POINT1
```

DSSPEAKER\_7POINT1\_ブロックの挿入は、コントロール パネルの 新しいホーム シアターを 7.1 スピーカーの構成を表します。 DSSPEAKER\_7POINT1 と DSSPEAKER\_7POINT1\_ワイド同じ全体の構成を 7.1 スピーカー構成の両方の名前が。

DirectSound のスピーカーの構成の詳細については、次を参照してください。 [DirectSound スピーカー構成設定](directsound-speaker-configuration-settings.md)します。

 

 





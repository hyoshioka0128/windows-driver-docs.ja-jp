---
title: ストリーム クラス ミニドライバー通信への DirectShow フィルター
description: ストリーム クラス ミニドライバー通信への DirectShow フィルター
ms.assetid: d2122827-758c-4557-b2fd-8774179b5da4
keywords:
- グラフ構成 WDK ビデオ キャプチャ、DirectShow をフィルター処理します。
- DirectShow の WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c79b4b9634630f6a4972f8733373989808512576
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384744"
---
# <a name="directshow-filter-to-stream-class-minidriver-communication"></a>ストリーム クラス ミニドライバー通信への DirectShow フィルター


Win32 API を使用してビデオ キャプチャ ミニドライバー対話ユーザー モード DirectShow フィルター **DeviceIoControl**関数呼び出し。 これらの呼び出しでは、ストリーム要求のブロック (される Srb) に、Stream クラス インターフェイスでは翻訳され、処理のビデオ キャプチャ ミニドライバーに送信されます。 される Srb の 2 つのカテゴリがあります。される Srb 全般のデバイス レベルの制御に使用して、個々 のストリームに影響を与えるされる Srb します。 次の表は、各カテゴリの主要なされる Srb に表示されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>デバイス</th>
<th>[ストリーミング]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>プロパティ</p>
<div>
 
</div>
書き込み</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568204" data-raw-source="[&lt;strong&gt;SRB_SET_DEVICE_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568204)"><strong>SRB_SET_DEVICE_PROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568207" data-raw-source="[&lt;strong&gt;SRB_SET_STREAM_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568207)"><strong>SRB_SET_STREAM_PROPERTY</strong></a></p></td>
</tr>
<tr class="even">
<td><p>プロパティ</p>
<div>
 
</div>
Read</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568170" data-raw-source="[&lt;strong&gt;SRB_GET_DEVICE_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568170)"><strong>SRB_GET_DEVICE_PROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568175" data-raw-source="[&lt;strong&gt;SRB_GET_STREAM_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568175)"><strong>SRB_GET_STREAM_PROPERTY</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>[ストリーミング]</p>
<div>
 
</div>
書き込み</td>
<td><p>なし</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568220" data-raw-source="[&lt;strong&gt;SRB_WRITE_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568220)"><strong>SRB_WRITE_DATA</strong></a></p></td>
</tr>
<tr class="even">
<td><p>[ストリーミング]</p>
<div>
 
</div>
Read</td>
<td><p>なし</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568200" data-raw-source="[&lt;strong&gt;SRB_READ_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568200)"><strong>SRB_READ_DATA</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>[ファイル]</p>
<div>
 
</div>
[ストリーミング]</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568191" data-raw-source="[&lt;strong&gt;SRB_OPEN_STREAM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568191)"><strong>SRB_OPEN_STREAM</strong></a></p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>Close</p>
<div>
 
</div>
[ストリーミング]</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568165" data-raw-source="[&lt;strong&gt;SRB_CLOSE_STREAM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568165)"><strong>SRB_CLOSE_STREAM</strong></a></p></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p>作成</p>
<div>
 
</div>
表記</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568168" data-raw-source="[&lt;strong&gt;SRB_GET_DATA_INTERSECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568168)"><strong>SRB_GET_DATA_INTERSECTION</strong></a></p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>[Change]</p>
<div>
 
</div>
[ストリーミング]
<div>
 
</div>
状態</td>
<td><p>なし</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568210" data-raw-source="[&lt;strong&gt;SRB_SET_STREAM_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568210)"><strong>SRB_SET_STREAM_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

ビデオ キャプチャ フィルター、テレビやラジオ チューナー フィルター、テレビのオーディオ フィルター、およびクロスバーのフィルターなどのビデオ キャプチャ フィルター グラフの「フロント エンド」を構成するフィルターのビデオ キャプチャ フィルターだけは本当にカーネルのストリーミングに参加します。 その他のフィルターは、ビデオ キャプチャ ミニドライバー自体内のデバイス レベルのプロパティ セットの制御に使用されます。 したがって、テレビやラジオのチューニング、テレビのオーディオ、およびクロスバーをサポートするミニドライバーは、ストリームの各カーネル ピン公開されません。 これらのストリームは、ユーザー モードの構築、グラフのトポロジを作成するときにのみ存在します。

 

 





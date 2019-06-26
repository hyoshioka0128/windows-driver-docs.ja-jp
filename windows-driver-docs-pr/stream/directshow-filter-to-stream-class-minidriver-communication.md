---
title: ストリーム クラス ミニドライバー通信への DirectShow フィルター
description: ストリーム クラス ミニドライバー通信への DirectShow フィルター
ms.assetid: d2122827-758c-4557-b2fd-8774179b5da4
keywords:
- グラフ構成 WDK ビデオ キャプチャ、DirectShow をフィルター処理します。
- DirectShow の WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f90277bb9cd13e2fec097046492d29acb7367d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358449"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-device-property" data-raw-source="[&lt;strong&gt;SRB_SET_DEVICE_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-device-property)"><strong>SRB_SET_DEVICE_PROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-stream-property" data-raw-source="[&lt;strong&gt;SRB_SET_STREAM_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-stream-property)"><strong>SRB_SET_STREAM_PROPERTY</strong></a></p></td>
</tr>
<tr class="even">
<td><p>プロパティ</p>
<div>
 
</div>
Read</td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-device-property" data-raw-source="[&lt;strong&gt;SRB_GET_DEVICE_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-device-property)"><strong>SRB_GET_DEVICE_PROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-property" data-raw-source="[&lt;strong&gt;SRB_GET_STREAM_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-property)"><strong>SRB_GET_STREAM_PROPERTY</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>[ストリーミング]</p>
<div>
 
</div>
書き込み</td>
<td><p>なし</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-write-data" data-raw-source="[&lt;strong&gt;SRB_WRITE_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-write-data)"><strong>SRB_WRITE_DATA</strong></a></p></td>
</tr>
<tr class="even">
<td><p>[ストリーミング]</p>
<div>
 
</div>
Read</td>
<td><p>なし</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-read-data" data-raw-source="[&lt;strong&gt;SRB_READ_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-read-data)"><strong>SRB_READ_DATA</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>[ファイル]</p>
<div>
 
</div>
[ストリーミング]</td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-stream" data-raw-source="[&lt;strong&gt;SRB_OPEN_STREAM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-stream)"><strong>SRB_OPEN_STREAM</strong></a></p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>Close</p>
<div>
 
</div>
[ストリーミング]</td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-stream" data-raw-source="[&lt;strong&gt;SRB_CLOSE_STREAM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-stream)"><strong>SRB_CLOSE_STREAM</strong></a></p></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p>作成</p>
<div>
 
</div>
表記</td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-data-intersection" data-raw-source="[&lt;strong&gt;SRB_GET_DATA_INTERSECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-data-intersection)"><strong>SRB_GET_DATA_INTERSECTION</strong></a></p></td>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-stream-state" data-raw-source="[&lt;strong&gt;SRB_SET_STREAM_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-stream-state)"><strong>SRB_SET_STREAM_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

ビデオ キャプチャ フィルター、テレビやラジオ チューナー フィルター、テレビのオーディオ フィルター、およびクロスバーのフィルターなどのビデオ キャプチャ フィルター グラフの「フロント エンド」を構成するフィルターのビデオ キャプチャ フィルターだけは本当にカーネルのストリーミングに参加します。 その他のフィルターは、ビデオ キャプチャ ミニドライバー自体内のデバイス レベルのプロパティ セットの制御に使用されます。 したがって、テレビやラジオのチューニング、テレビのオーディオ、およびクロスバーをサポートするミニドライバーは、ストリームの各カーネル ピン公開されません。 これらのストリームは、ユーザー モードの構築、グラフのトポロジを作成するときにのみ存在します。

 

 





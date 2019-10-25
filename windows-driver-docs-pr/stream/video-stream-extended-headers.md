---
title: ビデオ ストリームの拡張ヘッダー
description: ビデオ ストリームの拡張ヘッダー
ms.assetid: 6540026c-a41a-49e2-a41f-fe64106408f5
keywords:
- ビデオキャプチャ WDK AVStream、拡張ヘッダー
- ビデオのキャプチャ WDK AVStream、拡張ヘッダー
- 拡張ヘッダー WDK ビデオキャプチャ
- ヘッダー WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80ccc8d328ee007d901a5ec3bd155b42e3fc9f02
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843663"
---
# <a name="video-stream-extended-headers"></a>ビデオ ストリームの拡張ヘッダー


ビデオキャプチャミニドライバーでは、出力ストリームの拡張ヘッダーを使用して、ストリームと現在のフレームコンテンツに関する補助的な情報を提供します。 たとえば、イメージストリームヘッダーは、現在のフレーム番号、ドロップされたフレーム数、およびフィールド極性フラグに関する情報を提供します。 各フレームが完了すると、ミニドライバーは、キャプチャされたフレームに関する補足情報を拡張ヘッダーに格納します。

Stream クラス video capture ミニドライバーは、 [**HW\_\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)の**StreamHeaderMediaSpecific**メンバーを**sizeof** one に設定することによって、この追加情報を pin に提供する機能を示します。次の2つの構造体の。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>構造名</th>
<th>目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info" data-raw-source="[&lt;strong&gt;KS_FRAME_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)"><strong>KS_FRAME_INFO</strong></a></p></td>
<td><p>フレーム数、ドロップフレーム数、フィールド極性フラグ、および DirectDraw サーフェイスハンドル。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info" data-raw-source="[&lt;strong&gt;KS_VBI_FRAME_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info)"><strong>KS_VBI_FRAME_INFO</strong></a></p></td>
<td><p>VBI 形式、channel change 情報、video standard。</p></td>
</tr>
</tbody>
</table>

 

ストリームクラスミニドライバーがこの追加情報を提供しない場合は、 **StreamHeaderMediaSpecific**を0に設定する必要があります。

**StreamHeaderMediaSpecific**で値を指定する場合の詳細については、「[ストリームのカテゴリ](stream-categories.md)」を参照してください。

 

 





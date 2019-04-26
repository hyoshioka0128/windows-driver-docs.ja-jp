---
title: ビデオ ストリームの拡張ヘッダー
description: ビデオ ストリームの拡張ヘッダー
ms.assetid: 6540026c-a41a-49e2-a41f-fe64106408f5
keywords:
- ビデオ キャプチャ WDK AVStream、拡張ヘッダー
- ヘッダーの拡張、ビデオの WDK AVStream のキャプチャ
- 拡張ヘッダー WDK ビデオのキャプチャします。
- ヘッダーの WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 175cdf1e81deccbfb9c2222a1d069c2e87e24072
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359606"
---
# <a name="video-stream-extended-headers"></a>ビデオ ストリームの拡張ヘッダー


ビデオ キャプチャ ミニドライバーでは、その出力ストリームに含まれる拡張のヘッダーを使用して、ストリームと現在のフレームの内容に関する補足情報を提供します。 たとえば、イメージ ストリーム ヘッダーは、現在のフレーム数、フレームのドロップ、およびフィールドの極性フラグの数に関する情報を提供します。 各フレームが完了したため、ミニドライバーは、キャプチャされたフレームに関する補足情報と拡張のヘッダーに格納します。

Stream クラス ビデオ キャプチャ ミニドライバーを設定して、pin の追加情報を提供する機能を示すため、 **StreamHeaderMediaSpecific**のメンバー、 [ **HW\_ストリーム\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff559697)構造体を**sizeof**以下の 2 つの構造体のいずれか。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>構造体名</th>
<th>目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567645" data-raw-source="[&lt;strong&gt;KS_FRAME_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567645)"><strong>KS_FRAME_INFO</strong></a></p></td>
<td><p>フレームの数、フレーム数、フィールドの極性フラグおよび DirectDraw surface ハンドルを削除します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567694" data-raw-source="[&lt;strong&gt;KS_VBI_FRAME_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567694)"><strong>KS_VBI_FRAME_INFO</strong></a></p></td>
<td><p>VBI 形式では、チャネルは、標準のビデオについてを変更します。</p></td>
</tr>
</tbody>
</table>

 

Stream クラスのミニドライバーがこの追加情報を提供していない場合に設定する必要があります**StreamHeaderMediaSpecific**をゼロにします。

値を指定する場合の詳細については**StreamHeaderMediaSpecific**を参照してください[Stream カテゴリ](stream-categories.md)します。

 

 





---
title: マイクロドライバーの機能
description: マイクロドライバーの機能
ms.assetid: 491b954a-8ffa-4899-8c7d-0aee409f4742
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08d8dfd1f773bc1bc65321850ec4bf0c750f9046
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840782"
---
# <a name="microdriver-functions"></a>マイクロドライバーの機能





Wia フラットドライブは、wia マイクロドライバー関数を呼び出すことによって、WIA サービスからの要求に応答します。 これらの関数は、ベンダーが提供するすべてのマイクロドライバで実装する必要があり、次の要素で構成されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-microentry" data-raw-source="[&lt;strong&gt;MicroEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-microentry)"><strong>マイクロエントリ</strong></a></p></td>
<td><p>WIA フラットドライバーによって送信されたコマンドに応答します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-scan" data-raw-source="[&lt;strong&gt;Scan&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-scan)"><strong>取り込む</strong></a></p></td>
<td><p>デバイスからデータを読み取り、そのデータを WIA フラットドライバーに返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-setpixelwindow" data-raw-source="[&lt;strong&gt;SetPixelWindow&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-setpixelwindow)"><strong>Setピクセルウィンドウ</strong></a></p></td>
<td><p>スキャンする領域を設定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





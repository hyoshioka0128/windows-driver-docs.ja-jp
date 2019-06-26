---
title: ENCAPIPARAM\_ピーク\_ビットレート
description: ENCAPIPARAM\_ピーク\_ビットレート
ms.assetid: 444a20e0-f3af-4dbc-9272-44e992e059e8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23d9cc133b18d3ea490580d6a6bed85bc334ec76
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384140"
---
# <a name="encapiparampeakbitrate"></a>ENCAPIPARAM\_ピーク\_ビットレート


## <span id="ddk_encapiparam_peak_bitrate_ks"></span><span id="DDK_ENCAPIPARAM_PEAK_BITRATE_KS"></span>


ENCAPIPARAM\_ビットレート プロパティを使用して、デバイスのサポートされている最大ビット レート (ビット/秒) の範囲について説明します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、VT\_で指定された、デバイスのビットレートのピーク時の UI4 階段状の範囲、 **PropertyItem.Values**のメンバー [ **KSPROPERTY\_セット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)構造体。

### <a name="comments"></a>コメント

ミニドライバーは、静的なを指定するかに必要な**PropertyItem.Values**プロパティ項目またはハンドルの基本的な説明がクエリをサポートし、値を入力します。 ミニドライバーは、このプロパティの既定値も指定する必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)、 [ **VIDEOENCODER\_ビットレート\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

 






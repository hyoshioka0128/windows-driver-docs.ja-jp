---
title: ENCAPIPARAM\_ピーク\_ビットレート
description: ENCAPIPARAM\_ピーク\_ビットレート
ms.assetid: 444a20e0-f3af-4dbc-9272-44e992e059e8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc0698c00fddfcbffa8c83ac153cd952640384a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843208"
---
# <a name="encapiparam_peak_bitrate"></a>ENCAPIPARAM\_ピーク\_ビットレート


## <span id="ddk_encapiparam_peak_bitrate_ks"></span><span id="DDK_ENCAPIPARAM_PEAK_BITRATE_KS"></span>


ENCAPIPARAM\_ビットレートプロパティは、デバイスのサポートされているピークビットレート (ビット/秒) の範囲を示すために使用されます。

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、VT\_UI4 がステップ実行された、デバイスのピークビットレートです **。値**は、 [**KSK プロパティ\_SET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)構造体です。

### <a name="comments"></a>コメント

ミニドライバーは、静的な Propertyitem を提供する必要が**あります。** プロパティ項目の説明を指定するか、基本サポートクエリを処理しての値を入力します。 ミニドライバーでは、このプロパティの既定値も指定する必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** *Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="see-also"></a>参照

[**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [ **videoencoder\_ビットレート\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

 






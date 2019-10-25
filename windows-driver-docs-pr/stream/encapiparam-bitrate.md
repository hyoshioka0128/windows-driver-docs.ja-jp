---
title: ENCAPIPARAM\_ビットレート
description: ENCAPIPARAM\_ビットレート
ms.assetid: a0fba9b3-7ce3-407d-b53f-fd54a50cbdcb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c1c0e3493c70a15bd7e743a826e4ba17cae545a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843210"
---
# <a name="encapiparam_bitrate"></a>ENCAPIPARAM\_ビットレート


## <span id="ddk_encapiparam_bitrate_ks"></span><span id="DDK_ENCAPIPARAM_BITRATE_KS"></span>


ENCAPIPARAM\_ビットレートプロパティは、デバイスでサポートされるビットレート (ビット/秒) を示すために使用されます。

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

 

プロパティ値 (操作データ) は、デバイスでサポートされているビットレートの VT\_UI4 の段階的な範囲です **。値**は、 [**KSK プロパティ\_SET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)構造体に指定されています。

### <a name="comments"></a>コメント

このプロパティの使用方法のサンプルについては、「[エンコーダーコード例](https://docs.microsoft.com/windows-hardware/drivers/stream/encoder-code-examples)」を参照してください。

ミニドライバーは、静的な Propertyitem を提供する必要が**あります。** プロパティ項目の説明を指定するか、基本サポートクエリを処理しての値を入力します。 ミニドライバーでは、このプロパティの既定値も指定する必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** *Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="see-also"></a>参照

[**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [ **videoencoder\_ビットレート\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

 






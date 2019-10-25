---
title: ENCAPIPARAM\_ビットレート\_モード
description: ENCAPIPARAM\_ビットレート\_モード
ms.assetid: d7e82483-bee3-44bd-9066-c2877130a1f9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6888a00c10c960e5c0addb66c8e1d1cd23a01d96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843211"
---
# <a name="encapiparam_bitrate_mode"></a>ENCAPIPARAM\_ビットレート\_モード


## <span id="ddk_encapiparam_bitrate_mode_ks"></span><span id="DDK_ENCAPIPARAM_BITRATE_MODE_KS"></span>


ENCAPIPARAM\_ビットレートプロパティは、デバイスのエンコードモードを表すために使用されます。

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
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、 **Propertyitem. Values**メンバーで指定された VT\_I4 値です。値は、ksk プロパティの値のメンバーであり、videoencoder\_ビットレートからのサポートされている値の個別のリストを使用して、構造体[ **\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set) [ **@no__t8_ モード列挙体 (_s)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode) 。

### <a name="comments"></a>コメント

このプロパティの使用方法のサンプルについては、「[エンコーダーコード例](https://docs.microsoft.com/windows-hardware/drivers/stream/encoder-code-examples)」を参照してください。

ミニドライバーは、静的な Propertyitem を提供する必要が**あります。** プロパティ項目の説明を指定するか、基本サポートクエリを処理しての値を入力します。 ミニドライバーでは、このプロパティの既定値も指定する必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** *Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="see-also"></a>参照

[**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [ **videoencoder\_ビットレート\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

 






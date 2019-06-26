---
title: ENCAPIPARAM\_ビットレート\_モード
description: ENCAPIPARAM\_ビットレート\_モード
ms.assetid: d7e82483-bee3-44bd-9066-c2877130a1f9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b575dd02c77fb58be26d4da106828c2588d4b14
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384143"
---
# <a name="encapiparambitratemode"></a>ENCAPIPARAM\_ビットレート\_モード


## <span id="ddk_encapiparam_bitrate_mode_ks"></span><span id="DDK_ENCAPIPARAM_BITRATE_MODE_KS"></span>


ENCAPIPARAM\_ビットレート プロパティを使用して、デバイスのエンコード モードについて説明します。

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
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、VT\_I4 の値で指定された、 **PropertyItem.Values**のメンバー、 [ **KSPROPERTY\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)不連続のサポートされている値の一覧を含む構造体、 [ **VIDEOENCODER\_ビットレート\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)列挙体。

### <a name="comments"></a>コメント

このプロパティを使用する方法のサンプルでは、次を参照してください。[エンコーダーのコード例](https://docs.microsoft.com/windows-hardware/drivers/stream/encoder-code-examples)します。

ミニドライバーは、静的なを指定するかに必要な**PropertyItem.Values**プロパティ項目またはハンドルの基本的な説明がクエリをサポートし、値を入力します。 ミニドライバーは、このプロパティの既定値も指定する必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)、 [ **VIDEOENCODER\_ビットレート\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

 






---
title: ENCAPIPARAM\_ビットレート
description: ENCAPIPARAM\_ビットレート
ms.assetid: a0fba9b3-7ce3-407d-b53f-fd54a50cbdcb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd0909ed9eab9fc349eb1125117c5a56c4472f5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384142"
---
# <a name="encapiparambitrate"></a>ENCAPIPARAM\_ビットレート


## <span id="ddk_encapiparam_bitrate_ks"></span><span id="DDK_ENCAPIPARAM_BITRATE_KS"></span>


ENCAPIPARAM\_ビットレート プロパティを使用して、デバイスでサポートされているビット レート (ビット/秒) について説明します。

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

 

プロパティの値 (データの操作) は、VT\_UI4 ステップで指定された、デバイスでサポートされているビット レートの範囲、 **PropertyItem.Values**のメンバー [ **KSPROPERTY\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)構造体。

### <a name="comments"></a>コメント

このプロパティを使用する方法のサンプルでは、次を参照してください。[エンコーダーのコード例](https://docs.microsoft.com/windows-hardware/drivers/stream/encoder-code-examples)します。

ミニドライバーは、静的なを指定するかに必要な**PropertyItem.Values**プロパティ項目またはハンドルの基本的な説明がクエリをサポートし、値を入力します。 ミニドライバーは、このプロパティの既定値も指定する必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)、 [ **VIDEOENCODER\_ビットレート\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

 






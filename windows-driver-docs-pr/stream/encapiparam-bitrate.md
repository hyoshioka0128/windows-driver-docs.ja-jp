---
title: ENCAPIPARAM\_ビットレート
description: ENCAPIPARAM\_ビットレート
ms.assetid: a0fba9b3-7ce3-407d-b53f-fd54a50cbdcb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ae8d8b65c7146bca14fda44ccf1b8374d1ea8c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536257"
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

 

プロパティの値 (データの操作) は、VT\_UI4 ステップで指定された、デバイスでサポートされているビット レートの範囲、 **PropertyItem.Values**のメンバー [ **KSPROPERTY\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff565617)構造体。

### <a name="comments"></a>コメント

このプロパティを使用する方法のサンプルでは、次を参照してください。[エンコーダーのコード例](https://msdn.microsoft.com/library/windows/hardware/ff559532)します。

ミニドライバーは、静的なを指定するかに必要な**PropertyItem.Values**プロパティ項目またはハンドルの基本的な説明がクエリをサポートし、値を入力します。 ミニドライバーは、このプロパティの既定値も指定する必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)、 [ **VIDEOENCODER\_ビットレート\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff568695)

 

 






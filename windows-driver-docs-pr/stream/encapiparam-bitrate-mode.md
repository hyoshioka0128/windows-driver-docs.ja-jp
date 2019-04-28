---
title: ENCAPIPARAM\_ビットレート\_モード
description: ENCAPIPARAM\_ビットレート\_モード
ms.assetid: d7e82483-bee3-44bd-9066-c2877130a1f9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18593d48db168d4a891b8fbe4691c956cbcaa9a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363668"
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

 

プロパティの値 (データの操作) は、VT\_I4 の値で指定された、 **PropertyItem.Values**のメンバー、 [ **KSPROPERTY\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff565617)不連続のサポートされている値の一覧を含む構造体、 [ **VIDEOENCODER\_ビットレート\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff568695)列挙体。

### <a name="comments"></a>コメント

このプロパティを使用する方法のサンプルでは、次を参照してください。[エンコーダーのコード例](https://msdn.microsoft.com/library/windows/hardware/ff559532)します。

ミニドライバーは、静的なを指定するかに必要な**PropertyItem.Values**プロパティ項目またはハンドルの基本的な説明がクエリをサポートし、値を入力します。 ミニドライバーは、このプロパティの既定値も指定する必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)、 [ **VIDEOENCODER\_ビットレート\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff568695)

 

 






---
title: CODECAPI\_SETALLDEFAULTS
description: CODECAPI\_SETALLDEFAULTS
ms.assetid: 6a50a75f-cbc5-487f-b2cd-34e89eb127a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c18ba4f9f5bf5b3f02da0c13f26a46171e47be37
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844724"
---
# <a name="codecapi_setalldefaults"></a>CODECAPI\_SETALLDEFAULTS


## <span id="ddk_codecapi_setalldefaults_ks"></span><span id="DDK_CODECAPI_SETALLDEFAULTS_KS"></span>


CODECAPI\_SETALLDEFAULTS プロパティは、ミニドライバーのすべての内部設定を既定の構成にリセットするために使用されます。

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
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

このプロパティセットに設定されたは、デバイスがすべての設定を既定値にリセットするトリガーです。

### <a name="comments"></a>コメント

このプロパティが設定されている場合、ミニドライバーでは、 [CODECAPI\_currentchangelist](codecapi-currentchangelist.md)の変更されたパラメーターのリスト全体をキャッシュする必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** *Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






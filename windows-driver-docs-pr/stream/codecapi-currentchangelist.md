---
title: CODECAPI\_CURRENTCHANGELIST リスト
description: CODECAPI\_CURRENTCHANGELIST リスト
ms.assetid: f783857f-d1a1-417f-8f69-198b6f328a69
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c83cbb7ab2f2968ee0f5c150244dacf6d8d9b24e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844725"
---
# <a name="codecapi_currentchangelist"></a>CODECAPI\_CURRENTCHANGELIST リスト


## <span id="ddk_codecapi_currentchangelist_ks"></span><span id="DDK_CODECAPI_CURRENTCHANGELIST_KS"></span>


CODECAPI\_CURRENTCHANGELIST プロパティは、 [CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)や[CODECAPI\_setalldefaults](codecapi-setalldefaults.md)など、前のプロパティ "set" 呼び出しで変更されたパラメーターを示すために使用されます。

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
<td><p>Guid の配列</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、Guid の配列です。

### <a name="comments"></a>コメント

プロパティ get 呼び出し:

アプリケーションが0以外のバッファーサイズでプロパティ get 呼び出しを行う場合、指定されたバッファーがデータブロックに対して小さすぎると、ミニドライバーはステータス\_バッファー\_\_小さすぎます。 返される項目がない場合、ミニドライバーは STATUS\_SUCCESS を返します。 それ以外の場合は、Guid のリストが返されます (つまり、sizeof (GUID) バイトが16バイトと等しい)。 返されるサイズは、リストの長さをバイト単位で示します (つまり、GUID \* sizeof (GUID) の数)。

プロパティセットの呼び出し:

変更された Guid の現在の一覧はリセットされます。

### <a name="requirements"></a>要件

**ヘッダー:** *Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="see-also"></a>参照

[**Ksproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [CODECAPI\_allsettings](codecapi-allsettings.md)、 [CODECAPI\_setalldefaults](codecapi-setalldefaults.md)

 

 






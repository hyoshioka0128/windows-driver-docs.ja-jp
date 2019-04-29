---
title: CODECAPI\_CURRENTCHANGELIST
description: CODECAPI\_CURRENTCHANGELIST
ms.assetid: f783857f-d1a1-417f-8f69-198b6f328a69
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ae314793bae53c9805e7b632533d181ee092ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329588"
---
# <a name="codecapicurrentchangelist"></a>CODECAPI\_CURRENTCHANGELIST


## <span id="ddk_codecapi_currentchangelist_ks"></span><span id="DDK_CODECAPI_CURRENTCHANGELIST_KS"></span>


CODECAPI\_など変更前のプロパティ「セット」呼び出しでパラメーターを示す CURRENTCHANGELIST プロパティが使用される[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)と[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)します。

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
<td><p>Guid の配列</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、Guid の配列です。

### <a name="comments"></a>コメント

プロパティの呼び出しを取得します。

アプリケーションは、0 以外のバッファー サイズを使用して呼び出しを取得するプロパティが場合、ミニドライバーは状態を返します\_バッファー\_すぎます\_小さなデータ ブロックに対して指定されたバッファーが小さすぎる場合。 返されるアイテムがない場合、ミニドライバーはステータスを返します\_成功します。 それ以外の場合に Guid のリストが返されます (つまり、sizeof(GUID) バイトが 16 バイト)。 返されるサイズ (バイト単位) のリストの長さは、(つまり、GUID の番号\*sizeof(GUID)) します。

プロパティの呼び出しを設定します。

現在の変更された Guid の一覧がリセットされます。

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>関連項目

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier), [CODECAPI\_ALLSETTINGS](codecapi-allsettings.md), [CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

 

 






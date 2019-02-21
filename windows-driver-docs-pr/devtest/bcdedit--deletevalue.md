---
title: BCDEdit/deletevalue
description: BCDEdit/deletevalue コマンドを削除しますか、Windows ブート構成データ ストア (BCD) からブート エントリのオプション (とその値) を削除します。
ms.assetid: 70833A12-B1F7-4AF6-952F-02A70718E870
ms.date: 05/21/2018
keywords:
- BCDEdit/deletevalue ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /deletevalue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f229284215ca334b4925d4bc83db5220c43b45d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531457"
---
# <a name="bcdedit-deletevalue"></a>BCDEdit/deletevalue


**BCDEdit/deletevalue**コマンドを削除または Windows のブート構成データ ストア (BCD) からのブート エントリのオプション (とその値) を削除します。 使用して、 **BCDEdit/deletevalue**コマンドを使用して追加されたオプションを削除する、 [ **BCDEdit/set** ](bcdedit--set.md)コマンド。 
``` syntax
     bcdedit  /deletevalue [{ID}] datatype  

   
```

設定したブート オプションの値を削除するには、使用、 **BCDEdit/deletevalue**コマンド。 使用するための一般的なシナリオ、 **BCDEdit/deletevalue**コマンドは、テストとドライバーをデバッグするときに、ブート エントリのオプションを削除します。 

たとえば、 [ **BCDEdit/set** ](bcdedit--set.md)を変更する、**サイズ**プロセッサ グループのオプションをテストするための新しい値にするため、使用することができます**BCDEdit/deletevalue**を新しい値を削除し、既定値に戻すには、次のコマンドを入力します。 変更を反映するには、コンピューターを再起動する必要がありますしことに注意してください。

``` syntax
bcdedit /deletevalue groupsize
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows Vista</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
</tbody>
</table>

<a name="see-also"></a>関連項目
--------

[**BCDEdit/set**](bcdedit--set.md)
 

 






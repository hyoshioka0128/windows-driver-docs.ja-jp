---
title: logexts.logc
description: Logexts.logc 拡張機能 API のすべてのカテゴリが表示されます、特定のカテゴリ内のすべての Api を表示しますまたはでき、Api の 1 つまたは複数のカテゴリのログ記録を無効にします。
ms.assetid: b0132055-da13-45a8-8e83-06ddcb8b90d7
keywords:
- デバッグ logexts.logc Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e773d11624b197bf26fb1bb0ca0811e82d90924c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336126"
---
# <a name="logextslogc"></a>!logexts.logc


**! Logexts.logc**拡張機能 API のすべてのカテゴリが表示されます、特定のカテゴリのすべての Api を表示またはにより、および Api の 1 つまたは複数のカテゴリのログ記録を無効にします。

```dbgcmd
!logexts.logc e Categories 
!logexts.logc d Categories 
!logexts.logc p Category 
!logexts.logc 
```

## <a name="span-idddklogextslogcdbgspanspan-idddklogextslogcdbgspanparameters"></a><span id="ddk__logexts_logc_dbg"></span><span id="DDK__LOGEXTS_LOGC_DBG"></span>パラメーター


<span id="_______e______"></span><span id="_______E______"></span> **e**   
指定したカテゴリのログ記録を有効にします。

<span id="_______d______"></span><span id="_______D______"></span> **D**   
指定したカテゴリのログ記録を無効にします。

<span id="_______Categories______"></span><span id="_______categories______"></span><span id="_______CATEGORIES______"></span> *カテゴリ*   
有効または無効にするカテゴリを指定します。 複数のカテゴリが表示されている場合は、空白で区切ります。 アスタリスク (\*) をすべてのカテゴリを示すために使用できます。

<span id="_______p______"></span><span id="_______P______"></span> **p**   
指定したカテゴリに属するすべての Api を表示します。

<span id="_______Category______"></span><span id="_______category______"></span><span id="_______CATEGORY______"></span> *カテゴリ*   
Api が表示されるカテゴリを指定します。 1 つだけのカテゴリを指定することができます、 **p**オプション。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。 [Logger と LogViewer](logger-and-logviewer.md)します。

<a name="remarks"></a>注釈
-------

任意のオプションを指定せず **! logexts.logc**現在利用可能なカテゴリの一覧が表示され、どれを有効または無効には、します。

カテゴリが無効になっている場合、パフォーマンスのオーバーヘッドが不要になったのでそのカテゴリ内のすべての Api のフックは削除されます。 COM のフックは削除されません、ために再度有効にできません。

特定のカテゴリのみを有効にするは、特定の種類 (たとえば、ファイル操作) の Windows でプログラムのある相互作用の興味のあるのみときに役立ちます。 これにより、ログ ファイルのサイズを減少し、ロガーがプロセスの実行速度に与える影響も減少します。

次のコマンドは、すべてのカテゴリのログ記録を有効になります。

```dbgcmd
0:000> !logexts.logc e *
```

次のコマンドは、7 のカテゴリのログ記録を無効になります。

```dbgcmd
0:000> !logexts.logc d 7
```

次のコマンドは、13、15 のカテゴリのログ記録を有効になります。

```dbgcmd
0:000> !logexts.logc e 13 15
```

カテゴリ 3 に属しているすべての Api は、次のコマンドが表示されます。

```dbgcmd
0:000> !logexts.logc p 3
```

 

 






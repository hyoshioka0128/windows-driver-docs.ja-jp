---
title: gle
description: Gle 拡張機能では、現在のスレッドの最後のエラー値が表示されます。
ms.assetid: bed3ce17-6860-421f-ae20-11faa50310ed
keywords:
- スレッド、エラー値
- エラー値
- Windows デバッグ gle
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cf1b650d02b6abc31e9e8aa8c29e2ccb410603c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336593"
---
# <a name="gle"></a>!gle


**! Gle**拡張機能は、現在のスレッドの最後のエラー値を表示します。

```dbgcmd
!gle [-all]
```

## <a name="span-idddkgledbgspanspan-idddkgledbgspanparameters"></a><span id="ddk__gle_dbg"></span><span id="DDK__GLE_DBG"></span>パラメーター


<span id="_______-all______"></span><span id="_______-ALL______"></span> **-すべて**   
ターゲット システム上のユーザー モード スレッドごとの最後のエラーを表示します。 ユーザー モードでは、このパラメーターを省略した場合、デバッガーには、現在のスレッドの最後のエラーが表示されます。 カーネル モードでは、このパラメーターを省略すると、デバッガーを表示するスレッドの最後のエラーを現在[コンテキストを登録](changing-contexts.md#register-context)を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Ext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、 [ **GetLastError** ](https://msdn.microsoft.com/library/windows/desktop/ms679360)ルーチン、Micorosft Windows SDK のドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

**! Gle**拡張機能の値を表示する[ **GetLastError** ](https://msdn.microsoft.com/library/windows/desktop/ms679360)この値をデコードしようとします。

カーネル モードで、 **! gle**デバッガー スレッド環境ブロックの終了を読み取ることができる場合にのみ拡張機能の作業です。

 

 






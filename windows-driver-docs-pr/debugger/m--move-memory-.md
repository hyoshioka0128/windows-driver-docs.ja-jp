---
title: m (移動メモリ)
description: M コマンドは、1 つの場所から別にメモリの内容をコピーします。 このコマンドを混同しないでください、~ (スレッドの再開) m コマンド。
ms.assetid: afcac933-6bba-4566-ae07-bb9110f851d2
keywords:
- m (移動メモリ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- m (Move Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 837478b76e8307f050d9e4e9a6a0064acef5e74a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538402"
---
# <a name="m-move-memory"></a>m (移動メモリ)


**M**コマンドが 1 つの場所から別にメモリの内容をコピーします。

このコマンドを混同しないでください、 [ **~ (スレッドの再開) m** ](-m--resume-thread-.md)コマンド。

```dbgcmd
m Range Address 
```

## <a name="span-idddkcmdmovememorydbgspanspan-idddkcmdmovememorydbgspanparameters"></a><span id="ddk_cmd_move_memory_dbg"></span><span id="DDK_CMD_MOVE_MEMORY_DBG"></span>パラメーター


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
コピーするメモリ領域を指定します。 このパラメーターの構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
コピー先のメモリ領域の開始アドレスを指定します。 このパラメーターの構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

メモリの操作とその他のメモリに関連するコマンドの説明の詳細については、[読み取りと書き込みメモリ](reading-and-writing-memory.md)を参照してください。

<a name="remarks"></a>注釈
-------

メモリ領域を*アドレス*を指定します、メモリ領域の一部にすることができますを*範囲*を指定します。 重複する移動は正しく処理されます。

 

 






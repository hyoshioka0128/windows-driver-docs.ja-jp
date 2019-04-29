---
title: .dvfree (メモリの解放)
description: .Dvfree コマンドでは、ターゲット プロセスが所有するメモリの割り当てを解放します。
ms.assetid: 46845a5c-6ec4-4ae4-b89d-886df367dc5e
keywords:
- .dvfree (空きメモリ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dvfree (Free Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e65add81d64a3818c45061001879a5692f30f72a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334553"
---
# <a name="dvfree-free-memory"></a>.dvfree (メモリの解放)


**.Dvfree**コマンドは、ターゲット プロセスが所有するメモリの割り当てを解放します。

```dbgcmd
.dvfree [/d] BaseAddress Size 
```

## <a name="span-idddkmetafreememorydbgspanspan-idddkmetafreememorydbgspanparameters"></a><span id="ddk_meta_free_memory_dbg"></span><span id="DDK_META_FREE_MEMORY_DBG"></span>パラメーター


<span id="________d______"></span><span id="________D______"></span> **/d**   
割り当てがデコミットされるが、割り当てを含むページが実際には解放されません。 このオプションを使用する場合、デバッガーが呼び出す**VirtualFreeEx**で、 *dwFreeType*パラメーターと等しいメモリ最適化\_デコミットします。 このオプションを使用しない場合、値のメモリ最適化\_リリースを使用します。 詳細については、Microsoft Windows SDK を参照してください。

<span id="_______BaseAddress______"></span><span id="_______baseaddress______"></span><span id="_______BASEADDRESS______"></span> *BaseAddress*   
割り当ての先頭の仮想アドレスを指定します。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *サイズ*   
(バイト単位) を解放するメモリの量を指定します。 実際のメモリの解放を全体のメモリ ページ数と常になります。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**.Dvfree**コマンド呼び出し**VirtualFreeEx**を既存のメモリ割り当てを解放します。 しない限り、 **/d**オプションを指定すると、このメモリを含むページが解放されます。

このコマンドはによって行われた割り当てを解放できます[ **.dvalloc (メモリを割り当てる)**](-dvalloc--allocate-memory-.md)します。 ターゲット プロセスが所有するメモリが解放のメモリを使用して取得されませんでしたの任意のブロックを解放するためも使用できます **.dvalloc**ターゲット プロセスの安定性のリスクが自然です。

 

 






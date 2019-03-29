---
title: .dvalloc (メモリの割り当て)
description: .Dvalloc コマンドでは、ターゲット プロセスに追加のメモリの割り当てに Windows を実行します。
ms.assetid: 5bb0660e-0c88-4100-91ae-cd89834174f6
keywords:
- .dvalloc (メモリの割り当て) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dvalloc (Allocate Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de3632868528e71ccb078994bef77aee64d83709
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582049"
---
# <a name="dvalloc-allocate-memory"></a>.dvalloc (メモリの割り当て)


**.Dvalloc**コマンドは、ターゲット プロセスに追加のメモリの割り当てに Windows を実行します。

```dbgcmd
.dvalloc [Options] Size 
```

## <a name="span-idddkmetaallocatememorydbgspanspan-idddkmetaallocatememorydbgspanparameters"></a><span id="ddk_meta_allocate_memory_dbg"></span><span id="DDK_META_ALLOCATE_MEMORY_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の数を指定できます。

<span id="_b_BaseAddress"></span><span id="_b_baseaddress"></span><span id="_B_BASEADDRESS"></span>**/b** **** *BaseAddress*  
割り当ての先頭の仮想アドレスを指定します。

<span id="_r"></span><span id="_R"></span>**/r**  
メモリ、仮想アドレス空間で予約が、実際に物理メモリの割り当てはありません。 このオプションを使用する場合、デバッガーが呼び出す**VirtualAllocEx**で、 *flAllocationType*パラメーターと等しいメモリ最適化\_予約します。 このオプションを使用しない場合、値のメモリ最適化\_COMMIT |メモリ最適化\_予約を使用します。 詳細については、Microsoft Windows SDK を参照してください。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *サイズ*   
バイト単位で割り当てられるメモリの量を指定します。 プログラムに使用可能なメモリの量が等しくなる*サイズ*します。 実際に使用されるメモリ量があります少し大きくなりますが、あるため、これは常に全体のページ数です。

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

 

<a name="remarks"></a>コメント
-------

**.Dvalloc**コマンド呼び出し**VirtualAllocEx**ターゲット プロセスを新しいメモリを割り当てられません。 割り当てられたメモリは、読み取り、書き込み、および実行を許可します。

このメモリを解放するには、次のように使用します。 [ **.dvfree (空きメモリ)**](-dvfree--free-memory-.md)します。

 

 






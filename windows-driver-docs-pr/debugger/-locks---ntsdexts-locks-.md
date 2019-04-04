---
title: locks ntsdexts.locks
description: Ntsdexts.dll でロックの拡張機能では、現在のプロセスに関連付けられているクリティカル セクションの一覧が表示されます。この拡張機能のコマンドは、kdext*.locks 拡張機能のコマンドと混同しないでください。
ms.assetid: f33a68e8-1ddc-4d49-bb22-8f8b097c8ada
keywords:
- ロック (ntsdexts.locks) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- locks ( ntsdexts.locks)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5947ac71adbfde2a2a85e7fee0adcf05bd69145a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558874"
---
# <a name="locks-ntsdextslocks"></a>!locks (!ntsdexts.locks)


**! ロック**Ntsdexts.dll で拡張機能は、現在のプロセスに関連付けられているクリティカル セクションの一覧を表示します。

この拡張機能のコマンドと混同しないで、 [ **! kdext\*.locks** ](-locks---kdext--locks-.md)拡張機能コマンド。

```dbgcmd
    !locks [Options] 
```

## <a name="span-idddkntsdextslocksdbgspanspan-idddkntsdextslocksdbgspanparameters"></a><span id="ddk__ntsdexts_locks_dbg"></span><span id="DDK__NTSDEXTS_LOCKS_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
表示される情報の量を指定します。 次のオプションの任意の組み合わせを使用できます。

<span id="-v"></span><span id="-V"></span>**-v**  
すべての重要なセクションが含まれますが、現在所有していないを含め、表示をによりします。

<span id="-o"></span><span id="-O"></span>**-o**  
孤立した情報 (有効な重要なセクションを実際に指していないポインター) だけを表示をによりします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコマンドとクリティカル セクションの情報を表示できる拡張機能では、[クリティカル セクションを表示する](displaying-a-critical-section.md)を参照してください。 重要なセクションについては、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

この拡張機能のコマンドは、呼び出すことによって初期化されているすべての重要なセクションを示しています。 **RtlInitializeCriticalSection**します。 クリティカル セクションが存在しない場合は、出力が発生しません。

以下に例を示します。

```dbgcmd
0:000> !locks

CritSec w3svc!g_pWamDictator+a0 at 68C2C298
LockCount          0
RecursionCount     1
OwningThread       d1
EntryCount         1
ContentionCount    0
*** Locked

CritSec SMTPSVC+66a30 at 67906A30
LockCount          0
RecursionCount     1
OwningThread       d0
EntryCount         1
ContentionCount    0
*** Locked
```

 

 






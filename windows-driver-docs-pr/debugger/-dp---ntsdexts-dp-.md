---
title: dp ( ntsdexts.dp)
description: Ntsdexts.dll dp の拡張機能では、CSR プロセスが表示されます。
ms.assetid: 9e489cfc-2105-4605-b94d-88eea7883420
keywords:
- dp ( ntsdexts.dp) Windows Debugging
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dp ( ntsdexts.dp)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0d446a9e9f0ddf20f60e73e045875c1bf1843ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582047"
---
# <a name="dp-ntsdextsdp"></a>!dp (!ntsdexts.dp)


**! Dp** Ntsdexts.dll で拡張機能には、CSR プロセスが表示されます。

この拡張機能のコマンドと混同しないで、 [ **dp (表示メモリ)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンド、または、 [ **! kdext\*.dp** ](-db---dc---dd---dp---dq---du---dw.md)拡張機能コマンド。

```dbgcmd
!dp [v] [ PID | CSR-Process ]
```

## <a name="span-idddkntsdextsdpdbgspanspan-idddkntsdextsdpdbgspanparameters"></a><span id="ddk__ntsdexts_dp_dbg"></span><span id="DDK__NTSDEXTS_DP_DBG"></span>パラメーター


<span id="_______v______"></span><span id="_______V______"></span> **v**   
詳細モード。 構造体とスレッドの一覧が表示をによりします。

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
CSR のプロセスのプロセス ID を指定します。

<span id="_______CSR-Process______"></span><span id="_______csr-process______"></span><span id="_______CSR-PROCESS______"></span> *CSR プロセス*   
CSR のプロセスの 16 進数のアドレスを指定します。

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

 

<a name="remarks"></a>コメント
-------

この拡張機能は、プロセスのアドレス、プロセス ID、シーケンス番号、フラグ、および参照が表示されます。 カウントします。 詳細出力モードが選択されている場合は、追加の詳細が表示され、各プロセスのスレッドの情報が表示されます。

プロセスが指定されていない場合は、すべてのプロセスが表示されます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**!dt**](-dt.md)

 

 







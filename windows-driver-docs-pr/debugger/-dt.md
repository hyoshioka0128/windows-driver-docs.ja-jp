---
title: dt
description: Dt 拡張機能では、CSR のスレッドに関する情報が表示されます。この拡張機能のコマンドは、dt (表示の種類) コマンドと混同しないでください。
ms.assetid: 7fbca028-8d11-42b5-b64e-41eb3edc56cc
keywords:
- dt Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c806aa1c3f1bca241c2db492a1d02c8ec15cea5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556599"
---
# <a name="dt"></a>!dt


**! Dt**拡張機能は、CSR スレッドに関する情報を表示します。

この拡張機能のコマンドと混同しないで、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンド。

```dbgcmd
!dt [v] CSR-Thread 
```

## <a name="span-idddkdtdbgspanspan-idddkdtdbgspanparameters"></a><span id="ddk__dt_dbg"></span><span id="DDK__DT_DBG"></span>パラメーター


<span id="_______v______"></span><span id="_______V______"></span> **v**   
詳細モード。

<span id="_______CSR-Thread______"></span><span id="_______csr-thread______"></span><span id="_______CSR-THREAD______"></span> *CSR スレッド*   
CSR のスレッドの 16 進数のアドレスを指定します。

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

 

<a name="remarks"></a>注釈
-------

この拡張機能では、スレッド、プロセス、クライアント ID、フラグ、および CSR スレッドに関連付けられた参照カウントが表示されます。 詳細出力モードが選択されているもには、表示は、一覧のポインター、スレッドのハンドル、および待機のブロックに含まれます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**!dp (!ntsdexts.dp)**](-dp---ntsdexts-dp-.md)

 

 







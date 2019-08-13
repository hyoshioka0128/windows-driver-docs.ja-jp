---
title: error (エラー)
description: エラーの拡張機能では、デコードし、エラー値に関する情報が表示されます。
ms.assetid: 4999ab4b-2f55-47d4-b9a7-6f1231271fcc
keywords:
- エラー コード
- Win32 エラー コード
- WinSock エラー コード
- Windows デバッグ エラー
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- error
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 52979ccbfc69d9f31a38f833e4552d15e3e9a2d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334517"
---
# <a name="error"></a>!error


**!error**拡張機能をデコードし、エラー値に関する情報が表示されます。

```dbgcmd
!error Value [Flags]
```

## <a name="span-idddk__error_dbgspanspan-idddk__error_dbgspanparameters"></a><span id="ddk__error_dbg"></span><span id="DDK__ERROR_DBG"></span>パラメーター


<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *値*   
次のエラー コードのいずれかを指定します。

-   Win32

-   Winsock

-   NTSTATUS

-   NetAPI

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
場合*フラグ*設定されている NTSTATUS コードとして読み取りはエラー コードを 1 にします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

次の例を使用する方法を示します **! エラー**します。

```dbgcmd
0:000> !error 2
Error code: (Win32) 0x2 (2) - The system cannot find the file specified.
0:000> !error 2 1
Error code: (NTSTATUS) 0x2 - STATUS_WAIT_2
```

 

 






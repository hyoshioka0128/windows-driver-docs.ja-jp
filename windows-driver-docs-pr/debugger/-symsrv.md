---
title: symsrv 拡張コマンド
description: Symsrv 拡張機能は、シンボル サーバーのクライアントを閉じます。
ms.assetid: 666fa9d7-f723-4745-95fc-17aa20993b42
keywords:
- Windows デバッグ symsrv
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- symsrv
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 329178bf873560d7064569d0c5148f2c0d4770fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334211"
---
# <a name="symsrv"></a>!symsrv


**! Symsrv**拡張機能は、シンボル サーバーのクライアントを閉じます。

```dbgcmd
!symsrv close
```

## <span id="ddk__symsrv_dbg"></span><span id="DDK__SYMSRV_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**! Symsrv 閉じます**拡張機能は、アクティブなシンボル サーバーのクライアントを閉じます。

接続を再同期する必要がある場合に便利なことができます。

以前インターネット認証要求を拒否した場合は、使用する必要があります。 **! symsrv 閉じます**シンボル ストアに再接続します。 参照してください[ファイアウォールとプロキシ サーバー](firewalls-and-proxy-servers.md)詳細についてはします。

 

 






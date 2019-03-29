---
title: loadermemorylist
description: Loadermemorylist 拡張機能では、Windows では、Windows にローダー パスが起動メモリ割り当ての一覧が表示されます。
ms.assetid: 3e5dff7a-ea8f-4029-93e3-7c160487e968
keywords:
- OSLOADER
- Windows デバッグ loadermemorylist
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- loadermemorylist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fd3db55d67c45bfe3b7874407f0a9706c3c44ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571702"
---
# <a name="loadermemorylist"></a>!loadermemorylist


**! Loadermemorylist**拡張機能は、Windows では、Windows にローダー パスが起動メモリの割り当て一覧を表示します。

```dbgcmd
!loadermemorylist ListHeadAddress
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______ListHeadAddress______"></span><span id="_______listheadaddress______"></span><span id="_______LISTHEADADDRESS______"></span> *ListHeadAddress*   
リスト ヘッダーのアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p>
<p><strong>Windows Server 2003</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Vista 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

この拡張機能は、Ntldr が実行中にシステムのブート プロセスの開始時に使用する設計されています。 開始、終了、および各ページ範囲の種類を含むメモリ割り当ての一覧が表示されます。

任意の時点での実行を停止するには、CTRL + BREAK (WinDbg) で、または (KD) では、CTRL + C キーを押します。

 

 






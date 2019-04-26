---
title: errlog
description: Errlog 拡張機能には、I/O システムのエラー ログで、保留中のエントリの内容が表示されます。
ms.assetid: 2ef6331e-fa83-4515-8d70-5094e40b8497
keywords:
- Windows デバッグ errlog
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- errlog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4dc0b78c88df258019db1abd0da15c6404dc7774
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337217"
---
# <a name="errlog"></a>!errlog


**! Errlog**拡張機能は、I/O システムのエラー ログで、保留中のエントリの内容を表示します。

```dbgcmd
!errlog 
```

## <span id="ddk__errlog_dbg"></span><span id="DDK__ERRLOG_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

について[ **IoWriteErrorLogEntry**](https://msdn.microsoft.com/library/windows/hardware/ff550527)、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

このコマンドは、I/O システムのエラー ログに保留中のイベントに関する情報を表示します。 これらは、イベントへの呼び出しによってキューに入れ、 [ **IoWriteErrorLogEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff550527)が後続の表示のため、システムのイベント ログに書き込まれる、関数、**イベント ビューアー**します。

キューに置かれたエントリのみ[ **IoWriteErrorLogEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff550527)コミットされていないが、エラー ログが表示されます。

このコマンドは、システムが停止する前に、エラー ログにコミットできなかった保留中のエラー情報を表示するために、システム障害の後、診断を目的として使用できます。

 

 






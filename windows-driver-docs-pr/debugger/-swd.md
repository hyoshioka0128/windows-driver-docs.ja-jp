---
title: swd
description: Swd 拡張機能は、遅延プロシージャ呼び出し (DPC) およびスレッドのウォッチドッグ タイマーの状態を含む、指定されたプロセッサのソフトウェアのウォッチドッグ タイマー状態を表示します。
ms.assetid: 03532c7e-3bfc-4e37-8a0a-0a7c5a9963a8
keywords:
- ウォッチドッグのタイマー
- Windows デバッグ swd
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- swd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b00f32e34ef8729dbd2f5a690d965c9113e49c68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334217"
---
# <a name="swd"></a>!swd


**! Swd**拡張機能が遅延プロシージャ呼び出し (DPC) およびスレッドのウォッチドッグ タイマーの状態を含む、指定されたプロセッサのソフトウェアのウォッチドッグ タイマー状態を表示します。

```dbgcmd
!swd [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
プロセッサを指定します。 場合*プロセッサ*は省略すると、情報が、ターゲット コンピューター上のすべてのプロセッサに対して表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ウォッチドッグのタイマーがシャット ダウンまたは Windows では、応答が停止した場合は、Windows を再起動します。 時間は秒単位で表示されます。

 

 






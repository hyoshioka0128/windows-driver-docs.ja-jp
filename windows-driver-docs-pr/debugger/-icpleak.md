---
title: icpleak
description: Icpleak 拡張機能は、システム キューに置かれたエントリの最大数を持つオブジェクトのすべての I/O 完了オブジェクトを調べます。
ms.assetid: 8644a41a-44da-47bc-94ef-5024bb457c7d
keywords:
- I/O 完了
- Windows デバッグ icpleak
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- icpleak
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c3e1843dbcfee98d14985f06150abde7d18f94c3
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238371"
---
# <a name="icpleak"></a>!icpleak


**! Icpleak**拡張機能は、システム キューに置かれたエントリの最大数を持つオブジェクトのすべての I/O 完了オブジェクトを検査します。

```dbgcmd
!icpleak [HandleFlag]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______HandleFlag______"></span><span id="_______handleflag______"></span><span id="_______HANDLEFLAG______"></span> *HandleFlag*   
このフラグが設定されている場合、表示にはキューに置かれたエントリの最大数を持つオブジェクトを識別するハンドルのすべてのプロセスも含まれています。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

I/O 完了ポートについては、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

この拡張機能は、I/O 完了のプールでメモリ リークがある場合に便利です。 プロセスが呼び出すことによって I/O 完了のパケットを割り当てるときに、I/O 完了のプールのリークが発生する可能性が[ **PostQueuedCompletionStatus**](https://msdn.microsoft.com/library/windows/desktop/aa365458)、呼び出しはありませんが、 [ **GetQueuedCompletionStatus** ](https://msdn.microsoft.com/library/windows/desktop/aa364986) 、それらを解放するか、プロセスがキューに入れ、ポートに完了のエントリが、エントリを取得するスレッドは存在しません。 実行のリークを検出するために、 [ **! poolused** ](-poolused.md)プール タグの拡張機能と ICP の値を確認します。 プールが使用する場合、ICP タグは、重要でリークが発生した可能性があります。

この拡張機能は、システムの種類の一覧を管理する場合にのみ機能します。 場合、 *HandleFlag*設定は、システムに多数のプロセスに、この拡張機能には、実行に長い時間がかかります。

CTRL + BREAK (WinDbg) で、または (KD) で ctrl キーを押しながら C キーを押して任意の時点で停止できます。

 

 






---
title: dh
description: Dh の拡張機能は、指定したイメージのヘッダーを表示します。
ms.assetid: 1b4f94ae-42cc-4381-a2d1-c2f248e4d5a6
keywords:
- NTFS ファイル オブジェクト
- dh の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dh
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 409da4bb352fd554c6775a9e9a72b906c19de5f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334584"
---
# <a name="dh"></a>!dh


**! Dh**拡張機能には、指定したイメージのヘッダーが表示されます。

```dbgcmd
!dh [Options] Address 
!dh -h
```

## <a name="span-idddkdhdbgspanspan-idddkdhdbgspanparameters"></a><span id="ddk__dh_dbg"></span><span id="DDK__DH_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションのいずれか:

<span id="-f"></span><span id="-F"></span>**-f**  
ファイルのヘッダーを表示します。

<span id="-s"></span><span id="-S"></span>**-s**  
セクション ヘッダーを表示します。

<span id="-a"></span><span id="-A"></span>**-**  
すべてのヘッダー情報が表示されます。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
イメージの 16 進数のアドレスを指定します。

<span id="_______-h______"></span><span id="_______-H______"></span> **-h**   
この拡張機能のいくつかのヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Dbghelp.dll Kdextx86.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

[ **! Lmi** ](-lmi.md)拡張機能がイメージ ヘッダーから最も重要な情報を抽出し、簡潔な概要形式で表示します。 その拡張機能がより便利 **! dh**します。

 

 






---
title: ゾンビ
description: ゾンビの拡張機能では、すべての配信不能 (「ゾンビ」) のプロセスまたはスレッドが表示されます。
ms.assetid: f7fbce79-456a-4643-ad31-8cb2e6449ecf
keywords:
- Windows デバッグのゾンビ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- zombies
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5fecaaf6ca798764e3710631719dd3d34ded236e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573951"
---
# <a name="zombies"></a>!zombies


**! ゾンビ**拡張機能は、すべての配信不能 (「ゾンビ」) のプロセスまたはスレッドが表示されます。

```dbgcmd
!zombies [Flags [RestartAddress]]
```

## <a name="span-idddkzombiesdbgspanspan-idddkzombiesdbgspanparameters"></a><span id="ddk__zombies_dbg"></span><span id="DDK__ZOMBIES_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示される内容を指定します。 有効な値は次のとおりです。

<span id="1"></span>1  
ゾンビのすべてのプロセスを表示します。 (これは、既定値です)。

<span id="2"></span>2  
ゾンビのすべてのスレッドを表示します。

<span id="_______RestartAddress______"></span><span id="_______restartaddress______"></span><span id="_______RESTARTADDRESS______"></span> *RestartAddress*   
検索を開始する位置の 16 進数のアドレスを指定します。 これは、前回の検索が途中で終了した場合に役立ちます。 既定値は 0 です。

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
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

すべてのプロセスとスレッドの一覧を表示する、 [ **! プロセス**](-process.md)拡張機能。

プロセスとスレッドがカーネル モードの詳細については、[変更コンテキスト](changing-contexts.md)を参照してください。 プロセスとスレッドの分析に関する詳細については、*Microsoft Windows internals 』*、Mark Russinovich と David Solomon を参照してください。 (この本できない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>コメント
-------

ゾンビのプロセスとは、プロセスの一覧から削除されていない終了のプロセスです。 ゾンビのスレッドは似ています。

この拡張機能は、Windows 2000 でのみ使用できます。

 

 






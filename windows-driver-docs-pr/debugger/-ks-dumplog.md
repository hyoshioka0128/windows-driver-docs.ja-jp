---
title: ks.dumplog
description: Ks.dumplog 拡張機能では、内部のカーネル デバッグ ログのストリーミングが表示されます。
ms.assetid: 09829517-c01c-4cbd-bd0f-2ad0c1554f39
keywords:
- デバッグ ks.dumplog Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumplog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 48f08ad3b6950749f3300eb384680f94423a2780
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336304"
---
# <a name="ksdumplog"></a>!ks.dumplog


**! Ks.dumplog**拡張機能は、内部のカーネル デバッグ ログのストリーミングを表示します。

```dbgcmd
!ks.dumplog [Entries] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Entries______"></span><span id="_______entries______"></span><span id="_______ENTRIES______"></span> *エントリ*   
(省略可能)。 表示するログ エントリの数を指定します。 場合*エントリ*がゼロまたは省略すると、ログ全体が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>注釈
-------

ログの表示を停止するにはキーを押して[ **CTRL + C**](ctrl-c--break-.md)します。

この拡張機能では、対象のコンピュータがある必要があります Ks.sys のチェック (デバッグ) バージョンを実行します。

 

 






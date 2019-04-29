---
title: ks.dumpbag
description: Ks.dumpbag 拡張機能には、指定したオブジェクトのバッグ オブジェクトの内容が表示されます。
ms.assetid: a97b4794-b5dc-45a8-b1e9-5a626959020e
keywords:
- デバッグ ks.dumpbag Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumpbag
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fcedf397edb4a3f1fbfc529f87a23987b921620b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336325"
---
# <a name="ksdumpbag"></a>!ks.dumpbag


**! Ks.dumpbag**拡張機能は、指定したオブジェクトのバッグ オブジェクトの内容を表示します。

```dbgcmd
!ks.dumpbag Object [Level]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
有効なクライアントの表示可能なオブジェクトの構造体と、プライベート クラス オブジェクトへのポインターを指定します。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
(省略可能)。 0 ~ 7 で表示する詳細のレベルを指定の値を大きく表示徐々 に詳細なスケールします。 使用可能なすべての詳細を表示するには、7 の値を指定します。

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

次の例に示します、 **! ks.dumpbag**フィルターの表示。

```dbgcmd
kd> !dumpbag 829493c4
Filter 829493c4 [CKsFilter = 82949350]:
    Object Bag 829493d0:
        Object Bag Item 829dce28:
            Reference Count        : 1
            Item Cleanup Handler   : f7a21730
```

 

 






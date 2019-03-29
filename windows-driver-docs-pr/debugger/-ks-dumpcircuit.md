---
title: ks.dumpcircuit
description: Ks.dumpcircuit 拡張機能は、特定のオブジェクトに関連付けられたトランスポート回線の詳細を一覧表示します。
ms.assetid: 34e6fa0f-7479-4616-ba7e-f2b12ccc836d
keywords:
- デバッグ ks.dumpcircuit Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumpcircuit
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8167c78550aba9893f601632370aaa963faf98f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579764"
---
# <a name="ksdumpcircuit"></a>!ks.dumpcircuit


**! Ks.dumpcircuit**拡張機能は、特定のオブジェクトに関連付けられたトランスポート回線の詳細を一覧表示されます。

```dbgcmd
!ks.dumpcircuitextension Object [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
トランスポートの回線を表示するオブジェクトへのポインターを指定します。 AVStream の*オブジェクト*次の種類のいずれかを指定する必要があります。CKsPin\*、CKsQueue\*、CKsRequestor\*、CKsSplitter\*、CKsSplitterBranch\*します。

PortCls のオブジェクトは、次の種類のいずれかを指定する必要があります。CPortPin\*、CKsShellRequestor\*、または CIrpStream\*します。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
任意。 0 ~ 7 で表示する詳細のレベルを指定の値を大きく表示徐々 に詳細なスケールします。 使用可能なすべての詳細を表示するには、7 の値を指定します。

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

<a name="remarks"></a>コメント
-------

なお **! ks.dumpcircuit**データ ソースに常に対応していない、指定したオブジェクトで、回線のウォークを開始します。

最初に使用することができます[ **! ks.graph** ](-ks-graph.md)暗証番号 (pin) のアドレスの一覧表示しでこれらのアドレスを使用するフィルターのアドレスを持つ **! ks.dumpcircuit**します。

次の例に示します、 **! ks.dumpcircuit**表示。

```dbgcmd
kd> !dumpcircuit 8293f4f0
Pin8293f4f0 0 (snk, out)
Queue82990e20 r/w/c=2489/2/0
```

 

 






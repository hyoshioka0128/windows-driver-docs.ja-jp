---
title: wudfext.wudffile
description: Wudfext.wudffile 拡張機能には、フレームワーク ファイルに関する情報が表示されます。
ms.assetid: f655703d-0e61-4e9c-a033-834a89ef6d05
keywords:
- デバッグ wudfext.wudffile Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudffile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 19d7a0227b321310c8a00c0c98c923699ac51ad2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552292"
---
# <a name="wudfextwudffile"></a>!wudfext.wudffile


**! Wudfext.wudffile**拡張機能が framework ファイルに関する情報を表示します。

```dbgcmd
!wudfext.wudffile pWDFFile [TypeName] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______pWDFFile______"></span><span id="_______pwdffile______"></span><span id="_______PWDFFILE______"></span> *pWDFFile*   
アドレスを指定します、 **IWDFFile**インターフェイスに関する情報を表示します。

<span id="_______TypeName______"></span><span id="_______typename______"></span><span id="_______TYPENAME______"></span> *TypeName*   
(省略可能)。 インターフェイスの種類を指定します (たとえば、 **IWDFDevice**)。 場合の値を*TypeName*は省略すると、拡張機能は、値としてインターフェイスの型。 場合、アスタリスク (\*) として提供されている*TypeName*、場合*TypeName*は省略すると、拡張機能しようとすると、指定されたインターフェイスの種類を自動的に決定します。

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
<td align="left"><p><strong>Windows XP UMDF バージョン 1.7 以降</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)します。

 

 






---
title: wudfext.wudfusbinterface
description: Wudfext.wudfusbinterface 拡張機能では、USB インターフェイス オブジェクトに関する情報が表示されます。
ms.assetid: 4c93919a-781d-4bd8-9be2-eecdb75781b1
keywords:
- デバッグ wudfext.wudfusbinterface Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfusbinterface
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d7ccab3b154d474c02c55276f960e6e0faac2a93
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351584"
---
# <a name="wudfextwudfusbinterface"></a>!wudfext.wudfusbinterface


**! Wudfext.wudfusbinterface**拡張機能には、USB インターフェイス オブジェクトに関する情報が表示されます。

```dbgcmd
!wudfext.wudfusbinterface pWDFUSBInterface TypeName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______pWDFUSBInterface______"></span><span id="_______pwdfusbinterface______"></span><span id="_______PWDFUSBINTERFACE______"></span> *pWDFUSBInterface*   
アドレスを指定します、 **IWDFUsbInterface**インターフェイスに関する情報を表示します。 [ **! Wudfext.wudfobject** ](-wudfext-wudfobject.md)拡張機能コマンドのアドレスを決定する**IWDFUsbInterface**します。

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

 

 






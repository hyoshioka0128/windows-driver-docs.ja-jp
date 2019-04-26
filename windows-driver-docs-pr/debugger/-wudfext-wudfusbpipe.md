---
title: wudfext.wudfusbpipe
description: Wudfext.wudfusbpipe 拡張機能では、USB パイプ オブジェクトに関する情報が表示されます。
ms.assetid: a80f01e1-9c2c-4674-a067-0ff7e006713a
keywords:
- デバッグ wudfext.wudfusbpipe Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfusbpipe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 402dbbb3169cccf0121a06d227669b0d1f965a6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351528"
---
# <a name="wudfextwudfusbpipe"></a>!wudfext.wudfusbpipe


**! Wudfext.wudfusbpipe**拡張機能には、USB パイプ オブジェクトに関する情報が表示されます。

```dbgcmd
!wudfext.wudfusbpipe pWDFUSBPipe TypeName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______pWDFUSBPipe______"></span><span id="_______pwdfusbpipe______"></span><span id="_______PWDFUSBPIPE______"></span> *pWDFUSBPipe*   
アドレスを指定します、 **IWDFUsbTargetPipe**インターフェイスに関する情報を表示します。 [ **! Wudfext.wudfobject** ](-wudfext-wudfobject.md)拡張機能コマンドのアドレスを決定する**IWDFUsbTargetPipe**します。

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

 

 






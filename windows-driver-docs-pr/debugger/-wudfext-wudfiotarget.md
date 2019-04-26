---
title: wudfext.wudfiotarget
description: Wudfext.wudfiotarget 拡張機能には、ターゲットの状態および送信済み要求のリストを含む、I/O ターゲットに関する情報が表示されます。
ms.assetid: ccd241d6-c9c8-4518-902c-f119cf5b73fe
keywords:
- デバッグ wudfext.wudfiotarget Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfiotarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f4c50159c04826100e7e9fd6e36a3d8e5990731c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351378"
---
# <a name="wudfextwudfiotarget"></a>!wudfext.wudfiotarget


**! Wudfext.wudfiotarget**拡張機能は、ターゲットの状態と送信した要求の一覧を含む、I/O ターゲットに関する情報を表示します。

```dbgcmd
!wudfext.wudfiotarget pWDFTarget TypeName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______pWDFTarget______"></span><span id="_______pwdftarget______"></span><span id="_______PWDFTARGET______"></span> *pWDFTarget*   
アドレスを指定します、 **IWDFIoTarget**インターフェイスに関する情報を表示します。 [ **! Wudfext.wudfobject** ](-wudfext-wudfobject.md)拡張機能コマンドのアドレスを決定する**IWDFIoTarget**します。

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

 

 






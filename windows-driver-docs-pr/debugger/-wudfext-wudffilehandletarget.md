---
title: wudfext.wudffilehandletarget
description: Wudfext.wudffilehandletarget 拡張機能には、ファイル ハンドル ベースの I/O ターゲットに関する情報が表示されます。
ms.assetid: 14adf5ea-57d1-4ae5-8944-a643edd6ff39
keywords:
- デバッグ wudfext.wudffilehandletarget Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudffilehandletarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a47f0b19a0d49ca96924a410cd34f9fb1b826bfa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552476"
---
# <a name="wudfextwudffilehandletarget"></a>!wudfext.wudffilehandletarget


**! Wudfext.wudffilehandletarget**拡張機能は、ファイル ハンドル ベースの I/O ターゲットに関する情報を表示します。

```dbgcmd
!wudfext.wudffilehandletarget pWDFFileHandleTarget TypeName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______pWDFFileHandleTarget______"></span><span id="_______pwdffilehandletarget______"></span><span id="_______PWDFFILEHANDLETARGET______"></span> *pWDFFileHandleTarget*   
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

 

 






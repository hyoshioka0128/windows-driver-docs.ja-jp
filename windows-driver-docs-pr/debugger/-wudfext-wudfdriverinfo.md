---
title: wudfext.wudfdriverinfo
description: Wudfext.wudfdriverinfo 拡張機能には、現在のホスト プロセス内で UMDF ドライバーに関する情報が表示されます。
ms.assetid: 6204df00-2de5-41b6-80c1-ba576699fb20
keywords:
- デバッグ wudfext.wudfdriverinfo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdriverinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 42f87e0977ffec834ed692d9f485ce616379d4d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349102"
---
# <a name="wudfextwudfdriverinfo"></a>!wudfext.wudfdriverinfo


**! Wudfext.wudfdriverinfo**拡張機能には、現在のホスト プロセス内で UMDF ドライバーに関する情報が表示されます。

```dbgcmd
!wudfext.wudfdriverinfo Name
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名*   
に関する情報を表示、UMDF ドライバーの名前を指定します。

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
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

**! Wudfext.wudfdriverinfo**拡張機能は、各デバイス スタック内の各レベルを反復処理し、各エントリで指定する名前を持つドライバーと一致するドライバーとデバイスの情報が表示されます、 *名*パラメーター。

使用することができます **! wudfext.wudfdriverinfo**をすばやく、ドライバーのデバイス オブジェクトを検索します。

例を次に、 **! wudfext.wudfdriverinfo**表示。

```dbgcmd
kd> !wudfdriverinfo wudfechodriver 
IWDFDriver: 0xf2db8
  !WDFDEVICE 0xf2f80
    !devstack 0x34e4e0 @ level 0
```

 

 






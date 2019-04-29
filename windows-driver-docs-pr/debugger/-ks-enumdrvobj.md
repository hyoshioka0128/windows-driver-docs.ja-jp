---
title: ks.enumdrvobj
description: Ks.enumdrvobj 拡張機能は、指定した WDM ドライバー オブジェクトに関連付けられているすべての KSDEVICE 構造を表示し、フィルターの種類とこれらのデバイスで現在インスタンス化されたフィルターを一覧表示します。
ms.assetid: 8fcb8c83-48b6-402a-8374-6b1f0314837e
keywords:
- デバッグ ks.enumdrvobj Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.enumdrvobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cfd0360f4136e74d60ab14057f1ab0c725a7ba89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336323"
---
# <a name="ksenumdrvobj"></a>!ks.enumdrvobj


**! Ks.enumdrvobj**拡張機能、指定した WDM ドライバー オブジェクトに関連付けられているすべての KSDEVICE 構造を表示します。 フィルターの種類の一覧とフィルターをこれらのデバイスで現在インスタンス化します。

```dbgcmd
!ks.enumdrvobj DriverObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DriverObject______"></span><span id="_______driverobject______"></span><span id="_______DRIVEROBJECT______"></span> *DriverObject*   
WDM ドライバー オブジェクトへのポインターを指定します。

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

**! Ks.enumdrvobj** WDM ドライバー オブジェクトでは、オフにチェーンされているすべてのデバイスを列挙します呼び出しに相当[ **! ks.enumdevobj** ](-ks-enumdevobj.md)オフ チェーンされているすべてのデバイスで、指定された。ドライバー。

 

 






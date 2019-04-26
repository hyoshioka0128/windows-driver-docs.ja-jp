---
title: ks.enumdevobj
description: Ks.enumdevobj 拡張機能は、指定した WDM デバイス オブジェクトに関連付けられている KSDEVICE を表示し、このデバイス上で現在インスタンス化されたフィルターとフィルターの種類を一覧表示します。
ms.assetid: 3730fe3e-df7a-47fd-825b-ef31be6f7620
keywords:
- デバッグ ks.enumdevobj Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.enumdevobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ca40efafbe61729d7adb6ec86f0f3d4f253d7b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336293"
---
# <a name="ksenumdevobj"></a>!ks.enumdevobj


**! Ks.enumdevobj**拡張機能、指定した WDM デバイス オブジェクトに関連付けられている KSDEVICE を表示します。 フィルターの種類を一覧表示とこのデバイス上で現在インスタンス化をフィルター処理します。

```dbgcmd
!ks.enumdevobj DeviceObject 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
WDM デバイス オブジェクトへのポインターを指定します。

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

出力[ **! ks.allstreams** ](-ks-allstreams.md) 、入力として使用できる **! ks.enumdevobj**します。

次の例に示します、 **! ks.enumdevobj**表示。

```dbgcmd
kd> !enumdevobj 8241c020
WDM device object 8241c020:
    Corresponding KSDEVICE        823b8430
    Factory 829782dc [Descriptor f7a233c8] instances:
        829493c4 
```

 

 






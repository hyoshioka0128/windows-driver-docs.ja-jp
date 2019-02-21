---
title: ks.devhdr
description: Ks.devhdr 拡張機能では、デバイスのヘッダーを指定した WDM オブジェクトに関連付けられているストリーミング カーネルが表示されます。
ms.assetid: 1418ccfe-3842-422c-b2ce-124d0019d7b8
keywords:
- デバッグ ks.devhdr Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.devhdr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b2df61a97cf1b12eff226e84377116a7f514ad2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537229"
---
# <a name="ksdevhdr"></a>!ks.devhdr


**! Ks.devhdr**拡張機能には、デバイスのヘッダーを指定した WDM オブジェクトに関連付けられているストリーミング カーネルが表示されます。

```dbgcmd
!ks.devhdr DeviceObject 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
このパラメーターは、WDM デバイス オブジェクトへのポインターを指定します。 場合*デバイス オブジェクト*が無効で、コマンドには、エラーが返されます。

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

出力[ **! ks.allstreams** ](-ks-allstreams.md) 、入力として使用できる **! ks.devhdr**します。

次の例に示します、 **! ks.devhdr**表示。

```dbgcmd
kd> !devhdr 827aedf0 7
Device Header 824ca1e0
    Child Create Handler List:
        Create Item eb3a7284
            CreateFunction = sysaudio!CFilterInstance::FilterDispatchCreate+0x00 
            ObjectClass = NULL
            Flags = 0
```

 

 






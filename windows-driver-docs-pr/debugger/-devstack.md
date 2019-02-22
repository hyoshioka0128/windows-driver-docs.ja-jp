---
title: devstack
description: Devstack 拡張機能では、デバイス オブジェクトに関連付けられたデバイス スタックの書式設定されたビューが表示されます。
ms.assetid: 2215f166-2053-4525-80cd-be3817510dbd
keywords:
- Windows デバッグ devstack
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2c00bc4286dfcecf80f497e8ec6c8fa7ef9f28da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551454"
---
# <a name="devstack"></a>! devstack


**! Devstack**拡張機能には、デバイス オブジェクトに関連付けられたデバイス スタックの書式設定されたビューが表示されます。

```dbgcmd
!devstack DeviceObject 
```

## <a name="span-idddkdevstackdbgspanspan-idddkdevstackdbgspanparameters"></a><span id="ddk__devstack_dbg"></span><span id="DDK__DEVSTACK_DBG"></span>パラメーター


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
デバイス オブジェクトを指定します。 デバイスの 16 進数のアドレス指定できます\_オブジェクトの構造またはデバイスの名前。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

デバイス履歴の詳細については、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

場合*デバイス オブジェクト*デバイスの名前を指定しますが、プレフィックス、プレフィックスを提供しない"\\デバイス\\"と見なされます。 このコマンドでかどうかをチェックする注*デバイス オブジェクト*式エバリュエーターを使用する前に有効なアドレスまたはデバイス名は、します。

以下に例を示します。

```dbgcmd
kd> !devstack e000000085007b50
 !DevObj   !DrvObj            !DevExt   ObjectName
  e0000165fff32040  \Driver\kmixer     e0000165fff32190  
> e000000085007b50  \Driver\swenum     e000000085007ca0  KSENUM#00000005
!DevNode e0000165fff2e010 :
  DeviceInst is "SW\{b7eafdc0-a680-11d0-96d8-00aa0051e51d}\{9B365890-165F-11D0-A195-0020AFD156E4}"
 ServiceName is "kmixer"
```

 

 






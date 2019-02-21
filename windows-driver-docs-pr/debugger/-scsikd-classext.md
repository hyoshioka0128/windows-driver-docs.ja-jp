---
title: scsikd.classext
description: Scsikd.classext 拡張機能では、指定したクラスのプラグ アンド プレイ (PnP) デバイスが表示されます。
ms.assetid: 2b56966c-7ae1-4d44-ad60-19f31e47efff
keywords:
- デバッグ scsikd.classext Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- scsikd.classext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f96bc8d523df3f04e3bbf1905ed5576c2fdc6ae4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558038"
---
# <a name="scsikdclassext"></a>!scsikd.classext


**! Scsikd.classext**拡張機能には、指定したクラスのプラグ アンド プレイ (PnP) デバイスが表示されます。

```dbgcmd
!scsikd.classext [Device [Level]] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span> *デバイス*   
デバイス オブジェクトまたはクラスの PnP デバイスのデバイスの拡張機能を指定します。 場合*デバイス*は省略すると、すべてのクラスの PnP 拡張機能の一覧が表示されます。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
表示する詳細情報の量を指定します。 このパラメーターが取る 0、1、または 2 の値として 2 がほとんどの詳細情報を提供します。 既定値は 0 です。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Scsikd.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Scsikd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。 [SCSI ミニポート デバッグ](scsi-miniport-debugging.md)します。

<a name="remarks"></a>注釈
-------

次の例に示します、 **! scsikd.classext**表示。

```dbgcmd
0: kd> !scsikd.classext
  ' !scsikd.classext 8633e3f0 '   (             ) "IBM     " / "DDYS-T09170M    " / "S93E" / "        XBY45906"
  ' !scsikd.classext 86347b48 '   (paging device) "IBM     " / "DDYS-T09170M    " / "S80D" / "        VDA60491"
  ' !scsikd.classext 86347360 '   (             ) "UNISYS  " / "003451ST34573WC " / "5786" / "HN0220750000181300L6"
  ' !scsikd.classext 861d1898 '   (             ) "" / "MATSHITA CD-ROM CR-177" / "7T03" / ""

 usage: !classext <class fdo> <level [0-2]> 
```

 

 






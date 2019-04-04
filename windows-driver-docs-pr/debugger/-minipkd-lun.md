---
title: minipkd.lun
description: Minipkd.lun 拡張機能には、指定した論理ユニットの拡張機能 (LUN) に関する情報が表示されます。
ms.assetid: f78b2c15-ecfc-4138-b595-a6e3f0f7f93c
keywords:
- デバッグ minipkd.lun Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.lun
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 40bb448e3f0b7486be5406e984f2bd28355cdf21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560802"
---
# <a name="minipkdlun"></a>!minipkd.lun


**! Minipkd.lun**拡張機能には、指定した論理ユニットの拡張機能 (LUN) に関する情報が表示されます。

```dbgcmd
!minipkd.lun LUN 
!minipkd.lun Device 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______LUN______"></span><span id="_______lun______"></span> *LUN*   
LUN のアドレスを指定します。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span> *デバイス*   
LUN の物理デバイス オブジェクト (PDO) を指定します。

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
<td align="left"><p>Minipkd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[SCSI ミニポート デバッグ](scsi-miniport-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

LUN がすると通常呼ばれる、*デバイス*します。 したがって、この拡張機能では、アダプター上のデバイスに関する情報を表示します。

LUN は、そのアドレスでいずれかを指定 (に含まれている、 **LUN**のフィールド、 [ **! minipkd.adapters** ](-minipkd-adapters.md)表示)、または (物理デバイス オブジェクトが見つかった、 **DevObj**のフィールド、 **! minipkd.adapters**表示)。

 

 






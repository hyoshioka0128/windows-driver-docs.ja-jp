---
title: ks.automation
description: Ks.automation 拡張機能には、特定のオブジェクトに関連付けられたオートメーション項目が表示されます。
ms.assetid: a8fd790f-2793-4e6e-a500-f61646be2c89
keywords:
- デバッグ ks.automation Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.automation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f8a029c41e9f8c352ae6372d747580938837d96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336331"
---
# <a name="ksautomation"></a>!ks.automation


**! Ks.automation**拡張機能には、特定のオブジェクトに関連付けられたオートメーション項目が表示されます。

```dbgcmd
!ks.automation Object
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
オートメーション項目を表示する対象のオブジェクトへのポインターを指定します。 (オートメーション アイテム、プロパティ、メソッド、およびイベント)。*オブジェクト*次の種類のいずれかを指定する必要があります。PKSPIN、PKSFILTER、CKsPin\*、CKsFilter\*、PIRP します。 場合*オブジェクト*オートメーション コマンド プロパティ情報を返し、ハンドラーの IRP へのポインターです。

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

このコマンドを使用するにはから取得したフィルターのアドレスを持つ[ **! ks.enumdevobj**](-ks-enumdevobj.md)します。

次の例に示します、 **! ks.automation**を表示します。 引数は、フィルターのアドレスを示します。

```dbgcmd
kd> !automation 829493c4
Filter 829493c4 has the following automation items:
    Property Items:
        Set KSPROPSETID_Pin
            Item ID = KSPROPERTY_PIN_CINSTANCES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000008
            Item ID = KSPROPERTY_PIN_CTYPES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000004
            Item ID = KSPROPERTY_PIN_DATAFLOW
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000004
            Item ID = KSPROPERTY_PIN_DATARANGES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
            Item ID = KSPROPERTY_PIN_DATAINTERSECTION
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000028
                MinData = 00000000
            Item ID = KSPROPERTY_PIN_INTERFACES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
            Item ID = KSPROPERTY_PIN_MEDIUMS
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
            Item ID = KSPROPERTY_PIN_COMMUNICATION
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000004
            Item ID = KSPROPERTY_PIN_NECESSARYINSTANCES
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000004
            Item ID = KSPROPERTY_PIN_CATEGORY
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000010
            Item ID = KSPROPERTY_PIN_NAME
                Get Handler = ks!CKsFilter::Property_Pin
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
        Set KSPROPSETID_Topology
            Item ID = KSPROPERTY_TOPOLOGY_CATEGORIES
                Get Handler = ks!CKsFilter::Property_Topology
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000000
            Item ID = KSPROPERTY_TOPOLOGY_NODES
                Get Handler = ks!CKsFilter::Property_Topology
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000000
            Item ID = KSPROPERTY_TOPOLOGY_CONNECTIONS
                Get Handler = ks!CKsFilter::Property_Topology
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000000
            Item ID = KSPROPERTY_TOPOLOGY_NAME
                Get Handler = ks!CKsFilter::Property_Topology
                Set Handler = NULL
                MinProperty = 00000020
                MinData = 00000000
        Set KSPROPSETID_General
            Item ID = KSPROPERTY_GENERAL_COMPONENTID
                Get Handler = ks!CKsFilter::Property_General_ComponentId
                Set Handler = NULL
                MinProperty = 00000018
                MinData = 00000048
        Set [ks!KSPROPSETID_Frame]  a60d8368-5324-4893-b020-c431a50bcbe3
            Item ID = 0
                Get Handler = ks!CKsFilter::Property_Frame_Holding
                Set Handler = ks!CKsFilter::Property_Frame_Holding
                MinProperty = 00000018
                MinData = 00000004
    Method Items:
        NO SETS FOUND!
    Event Items:
        NO SETS FOUND!
```

 

 






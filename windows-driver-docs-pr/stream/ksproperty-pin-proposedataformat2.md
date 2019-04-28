---
title: KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2
description: OS の使用、KSPROPERTY\_暗証番号 (pin)\_PROPOSEDATAFORMAT2 プロパティのかどうかに、暗証番号 (pin) ファクトリによってピンがインスタンス化は、特定のデータ形式をサポートします。
ms.assetid: 64F6E8CA-8E48-43B3-9A60-DAB53516AD45
keywords:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT2 ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT2
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 12/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1a9148b21b1d9c5c3c49dcbd9de9a2e353371e4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380804"
---
# <a name="kspropertypinproposedataformat2"></a>KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2


OS の使用、 **KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**ドライバーが指定された属性を指定された pin で優先されるデータ形式であるかどうかを決定するプロパティ。

## <a name="usage-summary-table"></a>使用状況の概要テーブル


<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p>「解説」を参照してください。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561656" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561656)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロパティ記述子には、 [ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)続けて、 [ **KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)を指定する、可変サイズの数が続くを属性、 **KSMULTIPLE\_項目**します。 各属性が始まり、 [ **KSATTRIBUTE** ](https://msdn.microsoft.com/library/windows/hardware/ff560987)ヘッダーが、固有のデータ属性に続けています。 属性は、提案されたデータ形式を指定する、プロパティの要求のパラメーターとして機能します。

**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**型の構造体が含まれています[ **KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff561656)、

プロパティはサポートされている唯一の属性*KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_モード*を使用して指定されていると、 [ **KSATTRIBUTE\_AUDIOSIGNALPROCESSING\_モード**](https://msdn.microsoft.com/library/windows/hardware/mt727947)構造体。 なお、 **KSATTRIBUTE\_AUDIOSIGNALPROCESSING\_モード**構造体の始まりを[ **KSATTRIBUTE** ](https://msdn.microsoft.com/library/windows/hardware/ff560987)メンバー。 詳細については、次を参照してください。[オーディオ信号の処理モード](https://msdn.microsoft.com/library/windows/hardware/mt186386)します。

[**KSPROPERTY\_型\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)暗証番号 (pin) の形式が提示した場合にのみサポートします。 この関数は、指定した属性が指定された pin での既定のデータ形式に関する情報を提供するオーディオ ドライバーをできます。

KS フィルターは、暗証番号 (pin) に指定した属性の優先されるデータ形式が設定されている場合に STATUS_SUCCESS を返します。 ピン留めするには、指定した属性の優先されるデータ形式にいない場合は、STATUS_NOT_SUPPORTED を返します。 その他のエラーでは、適切なエラーが返されます。 ドライバーは、このプロパティをサポートする場合 OS は常に使用されている特定の信号の処理モードの次の形式を使用します。 KSPROPERTY_TYPE_SET はこのプロパティではサポートされていません。

**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2 入力構造体**

次の表は、KSPROPERTY の説明\_PIN\_PROPOSEDATAFORMAT2 入力構造*PinProperty*要素。

|                            |                                                                                                                                                                                    |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PinProperty.Property.Set   | PinProperty.Property.Set に設定する必要があります、 [KSPROPSETID\_Pin](kspropsetid-pin.md)要求されたモードにします。                                                                  |
| PinProperty.Property.Id    | 常に、PinProperty.Property.Id に設定する**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**します。                                                                                              |
| PinProperty.Property.Flags | PinProperty.Property.Flags を設定することができます[ **KSPROPERTY\_型\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)または KSPROPERTY\_型\_BASICSUPPORT basic を確認するにはプロパティに関する情報。 |
| PinProperty.PinId          | ターゲットの pin を識別する、PinProperty.PinId、 **KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**要求。                                                                           |
| PinProperty.Reserved       | PinProperty.Reserved では、将来使用するために予約されており、常にゼロ (0) に設定する必要があります。                                                                                          |

 

次の表は、KSPROPERTY の説明\_PIN\_PROPOSEDATAFORMAT2 入力構造*属性*要素。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Attributes.Count</td>
<td>属性は、通常 1 つ (1) の数、Attributes.Count を設定する必要があります。</td>
</tr>
<tr class="even">
<td>Attributes.Size</td>
<td>Attributes.Size は、ProposeDataformat2Input のサイズに設定する必要があります。 1 つの属性がある場合に、次のように計算できます。
<p>sizeof(ProposeDataformat2Input)</p></td>
</tr>
</tbody>
</table>

 

次の表は、KSPROPERTY の説明\_PIN\_PROPOSEDATAFORMAT2 入力構造*SignalProcessingModeAttribute*要素。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>SignalProcessingModeAttribute.AttributeHeader.Attribute</td>
<td>AttributeHeader.Attribute 要素は、必要な KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE に設定する必要があります。</td>
</tr>
<tr class="even">
<td>SignalProcessingModeAttribute.AttributeHeader.Flags</td>
<td>フラグ要素は、将来使用するために予約されており、常にゼロ (0) に設定する必要があります。</td>
</tr>
<tr class="odd">
<td>SignalProcessingModeAttribute.AttributeHeader.Size</td>
<td>サイズを示します、AttributeHeader.Size <a href="https://msdn.microsoft.com/library/windows/hardware/mt727947" data-raw-source="[&lt;strong&gt;KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt727947)"> <strong>KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE</strong></a>します。 これは、次のように計算できます。
<p>sizeof(KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE)</p></td>
</tr>
<tr class="even">
<td>SignalProcessingModeAttribute.SignalProcessingMode</td>
<td>SignalProcessingMode 要素は、要求された SIGNALPROCESSINGMODE AUDIO_SIGNALPROCESSINGMODE_DEFAULT などに設定する必要があります。</td>
</tr>
</tbody>
</table>

 

使用する**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**次の構造を定義します。

```cpp
typedef struct
{
    KSP_PIN                                 PinProperty;
    KSMULTIPLE_ITEM                         Attributes;
    KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE  SignalProcessingModeAttribute;
} ProposeDataformat2Input;
```

このコード サンプルでは、構造体を初期化する方法を示します。

```cpp
    ProposeDataformat2Input input = {0};

    input.PinProperty.Property.Set = KSPROPSETID_Pin;  
    input.PinProperty.Property.Id = KSPROPERTY_PIN_PROPOSEDATAFORMAT2;  
    input.PinProperty.Property.Flags = KSPROPERTY_TYPE_GET;  
    input.PinProperty.PinId = m_nPinId;  
    input.PinProperty.Reserved = 0;     

    input.Attributes.Count = 1;
    input.Attributes.Size = sizeof(ProposeDataformat2Input) - RTL_SIZEOF_THROUGH_FIELD(ProposeDataformat2Input, PinProperty);

    input.SignalProcessingModeAttribute.AttributeHeader.Attribute = KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE;
    input.SignalProcessingModeAttribute.AttributeHeader.Flags = 0;
    input.SignalProcessingModeAttribute.AttributeHeader.Size = sizeof(KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE);
    input.SignalProcessingModeAttribute.SignalProcessingMode = gProcessingMode;
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8.1 以降を利用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSDATAFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff561656)

 

 







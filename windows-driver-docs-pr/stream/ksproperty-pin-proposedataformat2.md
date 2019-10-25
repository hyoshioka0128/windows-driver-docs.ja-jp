---
title: KSK プロパティ\_PIN\_PROPOSEDATAFORMAT2
description: OS は KSK プロパティ\_ピン留め\_PROPOSEDATAFORMAT2 プロパティを使用して、pin ファクトリによってインスタンス化された pin が特定のデータ形式をサポートしているかどうかを判断します。
ms.assetid: 64F6E8CA-8E48-43B3-9A60-DAB53516AD45
keywords:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT2 ストリーミングメディアデバイス
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
ms.openlocfilehash: c2d293c802a2f930b6a2ed86fbe171752e072edc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838843"
---
# <a name="ksproperty_pin_proposedataformat2"></a>KSK プロパティ\_PIN\_PROPOSEDATAFORMAT2


OS は、 **Ksk プロパティ\_ピン留め\_PROPOSEDATAFORMAT2**プロパティを使用して、ドライバーが指定された属性を使用して pin に優先データ形式を持っているかどうかを判断します。

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>フィルター</p></td>
<td><p>「解説」を参照</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロパティ記述子は、 [**KSP\_のピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)の後に ksk の複数の[ **\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)が続き、 **ksmultiple\_項目**の後に続く可変サイズの属性の数を指定します。 各属性は、 [**Ksk 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute)ヘッダーの後に属性に固有のデータを指定して開始します。 属性は、提示されたデータ形式を指定して、プロパティ要求のパラメーターとして機能します。

**Ksk プロパティ\_PIN\_PROPOSEDATAFORMAT2**には、 [**KSPROPERTY\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)型の構造体が含まれています。

プロパティでサポートされている属性は、 *Ksk attributeid\_audiosignalprocessing\_mode*だけであり、 [**KSK 属性\_audiosignalprocessing\_mode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagksattribute_audiosignalprocessing_mode)構造体を使用して指定されています。 **Ksk 属性\_AUDIOSIGNALPROCESSING\_MODE**構造体は、 [**ksk 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute)メンバーで始まることに注意してください。 詳細については、「[オーディオ信号処理モード](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-signal-processing-modes)」を参照してください。

[**Ksk プロパティ\_TYPE\_GET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)は、pin の形式が提案されている場合にのみサポートされます。 この関数を使用すると、オーディオドライバーは、指定された属性を使用して、pin の既定のデータ形式に関する情報を提供できます。

指定された属性に対して pin に優先データ形式が指定されている場合、KS フィルターは STATUS_SUCCESS を返します。 指定した属性に対して pin に優先するデータ形式がない場合は、STATUS_NOT_SUPPORTED が返されます。 その他のエラーについては、適切なエラーが返されます。 ドライバーがこのプロパティをサポートしている場合、OS は常に特定のシグナル処理モードでこの形式を使用します。 KSPROPERTY_TYPE_SET は、このプロパティではサポートされていません。

**KSK プロパティ\_PIN\_PROPOSEDATAFORMAT2 入力構造体**

次の表は、PROPOSEDATAFORMAT2 入力構造の*pinproperty*要素を\_\_の ksk プロパティの説明を示しています。

|                            |                                                                                                                                                                                    |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PinProperty. Property. Set   | 要求されたモードでは、 [Pinpropsetid\_Pin](kspropsetid-pin.md)に設定する必要があります。                                                                  |
| PinProperty.Property.Id    | PinProperty.Property.Id は常に**Ksk プロパティ\_ピン\_PROPOSEDATAFORMAT2**に設定されます。                                                                                              |
| PinProperty. プロパティ。 Flags | プロパティに関する基本情報を確認するには、PinProperty. Property. Flags を[**Ksk プロパティ\_type\_GET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)または ksk プロパティ\_型\_basicsupport に設定できます。 |
| PinProperty. Pinproperty          | PinProperty. Pinproperty は、 **PROPOSEDATAFORMAT2 要求\_\_の Ksk プロパティ**のターゲットピンを識別します。                                                                           |
| PinProperty。予約済み       | PinProperty. 予約済みは将来の使用のために予約されており、常にゼロ (0) に設定する必要があります。                                                                                          |

 

次の表では、PROPOSEDATAFORMAT2 入力構造*属性*の要素\_をピン留めする KSK\_プロパティの説明を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Attributes. Count</td>
<td>Attributes. Count は、属性の数に設定する必要があります (通常は 1)。</td>
</tr>
<tr class="even">
<td>Attributes. Size</td>
<td>ProposeDataformat2Input のサイズに設定する必要があります。 属性が1つある場合、次のように計算できます。
<p>sizeof (ProposeDataformat2Input)</p></td>
</tr>
</tbody>
</table>

 

次の表では、PROPOSEDATAFORMAT2 入力構造の*Signalprocessingmodeattribute*要素を\_\_の ksk プロパティについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>SignalProcessingModeAttribute. AttributeHeader. 属性</td>
<td>AttributeHeader. Attribute 要素は、必要な KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE に設定する必要があります。</td>
</tr>
<tr class="even">
<td>SignalProcessingModeAttribute. AttributeHeader. Flags</td>
<td>Flags 要素は将来使用するために予約されており、常にゼロ (0) に設定する必要があります。</td>
</tr>
<tr class="odd">
<td>SignalProcessingModeAttribute. AttributeHeader.</td>
<td>AttributeHeader. Size は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagksattribute_audiosignalprocessing_mode" data-raw-source="[&lt;strong&gt;KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagksattribute_audiosignalprocessing_mode)"><strong>KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE</strong></a>のサイズを示します。 次のように計算できます。
<p>sizeof (KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE)</p></td>
</tr>
<tr class="even">
<td>SignalProcessingModeAttribute。 SignalProcessingMode</td>
<td>SignalProcessingMode 要素は、AUDIO_SIGNALPROCESSINGMODE_DEFAULT などの、要求された SIGNALPROCESSINGMODE に設定する必要があります。</td>
</tr>
</tbody>
</table>

 

Ksk プロパティを使用するには **\_ピン留め\_PROPOSEDATAFORMAT2**で次の構造を定義します。

```cpp
typedef struct
{
    KSP_PIN                                 PinProperty;
    KSMULTIPLE_ITEM                         Attributes;
    KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE  SignalProcessingModeAttribute;
} ProposeDataformat2Input;
```

このコードサンプルでは、構造体を初期化する方法を示します。

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
<td><p>Windows 8.1 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ピン留め**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

 

 







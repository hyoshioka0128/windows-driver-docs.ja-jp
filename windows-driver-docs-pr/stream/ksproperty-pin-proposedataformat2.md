---
title: KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2
description: OS は、KSK プロパティの \_ pin \_ PROPOSEDATAFORMAT2 プロパティを使用して、pin ファクトリによってインスタンス化された pin が特定のデータ形式をサポートしているかどうかを判断します。
ms.assetid: 64F6E8CA-8E48-43B3-9A60-DAB53516AD45
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_PIN_PROPOSEDATAFORMAT2
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
ms.openlocfilehash: 99cf580f118a5c33da5c5630365043a2976a186f
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968531"
---
# <a name="ksproperty_pin_proposedataformat2"></a>KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2


OS は、指定された属性を使用して、ドライバーの pin に優先データ形式があるかどうかを判断するために、 **ksproperty \_ PIN \_ PROPOSEDATAFORMAT2**プロパティを使用します。

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
<th>オン</th>
<th>Target</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>フィルター</p></td>
<td><p>「解説」を参照</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロパティ記述子は、 [**KSP の \_ PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)の後に **、ksmultiple \_ **項目の後に続く可変サイズの属性の数を指定する[**ksk 複数の \_ 項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)を指定します。 各属性は、 [**Ksk 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute)ヘッダーの後に属性に固有のデータを指定して開始します。 属性は、提示されたデータ形式を指定して、プロパティ要求のパラメーターとして機能します。

**Ksproperty \_ピン \_ PROPOSEDATAFORMAT2**には、 [**ksmultiple \_ ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)型の構造が含まれています。

プロパティでサポートされている属性は、 *Ksk attributeid \_ audiosignalprocessing \_ モード*のみです。この属性は、 [**ksattributeid \_ audiosignalprocessing \_ モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagksattribute_audiosignalprocessing_mode)構造体を使用して指定されています。 **Ksk 属性 \_ audiosignalprocessing \_ モード**構造体は、 [**ksattribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute)メンバーで開始することに注意してください。 詳細については、「[オーディオ信号処理モード](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-signal-processing-modes)」を参照してください。

[**Ksproperty \_TYPE \_ GET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)は、pin の形式が提案されている場合にのみサポートされます。 この関数を使用すると、オーディオドライバーは、指定された属性を使用して、pin の既定のデータ形式に関する情報を提供できます。

指定された属性に対して pin に優先データ形式が使用されている場合、KS フィルターは STATUS_SUCCESS を返します。 指定した属性に対して pin に優先するデータ形式がない場合は STATUS_NOT_SUPPORTED が返されます。 その他のエラーについては、適切なエラーが返されます。 ドライバーがこのプロパティをサポートしている場合、OS は常に特定のシグナル処理モードでこの形式を使用します。 KSPROPERTY_TYPE_SET は、このプロパティではサポートされていません。

**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2 入力構造体**

次の表では、KSK プロパティの \_ PIN \_ PROPOSEDATAFORMAT2 入力構造の*pinproperty*要素について説明します。

**Pinproperty. property. set**: 要求されたモードでは、 [pinpropsetid \_ Pin](kspropsetid-pin.md)に設定する必要があります。

**PinProperty.Property.Id**: PinProperty.Property.Id は常に**ksk プロパティの \_ PIN \_ PROPOSEDATAFORMAT2**に設定されます。

**Pinproperty. property. flags**: プロパティに関する基本情報を確認するには、値を[**ksk プロパティ \_ TYPE \_ GET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)または ksk プロパティ \_ 型 basicsupport に設定できます。 \_

Pinproperty **. pinproperty**: pinproperty. pinproperty は、 **ksproperty \_ pin \_ PROPOSEDATAFORMAT2**要求のターゲット pin を識別します。

**Pinproperty. 予約**済み: pinproperty。予約は将来使用するために予約されており、常にゼロ (0) に設定する必要があります。


 

次の表では、KSK プロパティの \_ PIN \_ PROPOSEDATAFORMAT2 入力構造*属性*の要素について説明します。

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

 

次の表では、KSK プロパティの \_ PIN \_ PROPOSEDATAFORMAT2 入力構造の*Signalprocessingmodeattribute*要素について説明します。

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
<td>AttributeHeader. サイズは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagksattribute_audiosignalprocessing_mode" data-raw-source="[&lt;strong&gt;KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagksattribute_audiosignalprocessing_mode)"><strong>KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE</strong></a>のサイズを示します。 次のように計算できます。
<p>sizeof (KSATTRIBUTE_AUDIOSIGNALPROCESSING_MODE)</p></td>
</tr>
<tr class="even">
<td>SignalProcessingModeAttribute。 SignalProcessingMode</td>
<td>SignalProcessingMode 要素は、AUDIO_SIGNALPROCESSINGMODE_DEFAULT のように、要求された SIGNALPROCESSINGMODE に設定する必要があります。</td>
</tr>
</tbody>
</table>

 

**Ksk プロパティの \_ PIN \_ PROPOSEDATAFORMAT2**を使用するには、次の構造を定義します。

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


[**KSP の \_ PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

 

 







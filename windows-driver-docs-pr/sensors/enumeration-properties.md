---
title: 列挙プロパティ
description: このトピックでは、PnP ドライバーストアから使用できる静的なセンサープロパティについて説明します。
ms.assetid: E4663410-375F-48B9-A9E4-6E608FA8D2FF
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8aab013ce15dabc077f9db23b4cc47454cdeac90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841688"
---
# <a name="enumeration-properties"></a>列挙プロパティ


このトピックでは、PnP ドライバーストアから使用できる静的なセンサープロパティについて説明します。

次の表は、静的なセンサーのプロパティを示しています。 [SensorsCxSensorCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensorcreate)が呼び出されると、クラス拡張 (CX) はセンサーごとにこれらのプロパティを書き込みます。 クライアントアプリケーションは、これらのプロパティを使用して、Windows デバイスでセンサーを検索できます。

**[型]** 列に表示されるデータ型の詳細については、「 [propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティキー</th>
<th>タスクバーの検索ボックスに</th>
<th>必須/オプション</th>
<th><strong>説明</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Type</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必須かどうか</p></td>
<td><p>センサーの種類を識別する GUID。 センサーの種類の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants" data-raw-source="[Sensor type GUIDs](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)">センサーの種類の guid</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_Category</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必須かどうか</p></td>
<td><p>センサーカテゴリ。 これは、デスクトップ v1 スタックとの下位互換性を維持するために必要です。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_ConnectionType</p></td>
<td><p>VT_UI4</p></td>
<td><p>オプション</p>
<p>アンビエント光センサーと加速度計に必要</p></td>
<td><p>Senor は接続の種類。 センサーの接続の種類は、統合、アタッチ、または外部にすることができます。</p>
<p>詳細については、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002" data-raw-source="[&lt;strong&gt;SensorConnectionType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002)"><strong>Sensorconnectiontype</strong></a>列挙体を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_IsPrimary</p></td>
<td><p>VT_BOOL</p></td>
<td><p>オプション</p></td>
<td><p>これがプライマリセンサーであることを示します。 設定されていない場合、既定値は false です。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Name</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>カスタムセンサーに必要です。</p></td>
<td><p>センサーの名前。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_Manufacturer</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>必須かどうか</p></td>
<td><p>センサーの製造元。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Model</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>必須かどうか</p></td>
<td><p>センサーのモデル。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_PersistentUniqueId</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必須かどうか</p></td>
<td><p>センサーを識別する GUID。 この値は、デバイス上の同じモデルのセンサーごとに一意である必要があります。 この要件は、内部および外部に接続されているセンサーの両方に適用されます。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_VendorDefinedSubType</p></td>
<td><p>VT_CLSID</p></td>
<td><p>カスタムセンサーに必要です。</p></td>
<td><p>ベンダーによって定義されたセンサーカテゴリのサブタイプを識別する GUID。</p>
<p>カスタムセンサー以外では、これは必要ありません。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_SensorData_LightLevel_AutoBrightnessPreferred</p></td>
<td><p>VT_BOOL</p></td>
<td><p>オプション</p></td>
<td><p>光センサーは、自動輝度調整に適しています。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_SensorData_LightLevel_ColorCapable</p></td>
<td><p>VT_BOOL</p></td>
<td><p>(省略可能)。 [度] と [光の温度] をサポートする場合は必須です。</p></td>
<td><p>光センサーは、光の気温と、またはその両方の x/y をサポートします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

[**SensorConnectionType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002)

[SensorsCxSensorCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensorcreate)

[センサーのプロパティ](sensor-properties2.md)

[センサーの種類の Guid](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)

 

 







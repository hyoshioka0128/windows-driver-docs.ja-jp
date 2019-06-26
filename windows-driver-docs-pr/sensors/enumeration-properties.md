---
title: 列挙プロパティ
description: このトピックでは、PnP ドライバー ストアから利用可能なセンサーの静的なプロパティについて説明します。
ms.assetid: E4663410-375F-48B9-A9E4-6E608FA8D2FF
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5bcd0470d4ae7a3498b5bdfe00df7034b810564e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386185"
---
# <a name="enumeration-properties"></a>列挙プロパティ


このトピックでは、PnP ドライバー ストアから利用可能なセンサーの静的なプロパティについて説明します。

次の表では、センサーの静的プロパティを示します。 クラスの拡張機能 (CX) は、各センサーのこれらのプロパティを書き込むときに[SensorsCxSensorCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensorcreate)が呼び出されます。 クライアント アプリケーションは、Windows デバイス上のセンサーを検索するこれらのプロパティを使用することができます。

示されるデータ型の詳細については、**型**列を参照してください[PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティのキー</th>
<th>種類</th>
<th>必須/オプション</th>
<th><strong>説明</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Type</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必須</p></td>
<td><p>センサーの種類を識別する GUID。 センサーの種類の詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants" data-raw-source="[Sensor type GUIDs](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)">センサーの種類の Guid</a>します。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_Category</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必須</p></td>
<td><p>センサーのカテゴリ。 これは旧バージョンと要件が、デスクトップの v1 スタックとの互換性です。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_ConnectionType</p></td>
<td><p>VT_UI4</p></td>
<td><p>省略可能</p>
<p>環境光センサー、加速度計に必要な</p></td>
<td><p>Senor 接続の種類。 センサーの接続の種類には、統合、接続されている、または外部を指定できます。</p>
<p>詳細については、次を参照してください。、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002" data-raw-source="[&lt;strong&gt;SensorConnectionType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002)"> <strong>SensorConnectionType</strong> </a>列挙体。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_IsPrimary</p></td>
<td><p>VT_BOOL</p></td>
<td><p>省略可能</p></td>
<td><p>これは、プライマリのセンサーを示します。 これは、既定値は設定されていない場合は、false です。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Name</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>カスタム センサーで必要です。</p></td>
<td><p>センサーの名前。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_Manufacturer</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>必須</p></td>
<td><p>センサーの製造元。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Model</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>必須</p></td>
<td><p>センサーのモデル。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_PersistentUniqueId</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必須</p></td>
<td><p>センサーを識別する GUID。 この値は、各センサーのデバイス上で同一モデルに対して一意である必要があります。 この要件は、両方の内部および外部で接続されたセンサーに適用されます。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_VendorDefinedSubType</p></td>
<td><p>VT_CLSID</p></td>
<td><p>カスタム センサーで必要です。</p></td>
<td><p>ベンダーによって定義されたセンサー カテゴリ サブタイプを識別する GUID。</p>
<p>非カスタム センサーでは、これは必要ありません。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_SensorData_LightLevel_AutoBrightnessPreferred</p></td>
<td><p>VT_BOOL</p></td>
<td><p>省略可能</p></td>
<td><p>自動明るさの光センサーお勧めします。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_SensorData_LightLevel_ColorCapable</p></td>
<td><p>VT_BOOL</p></td>
<td><p>(省略可能)。 一番と光の温度をサポートしている場合に必要です。</p></td>
<td><p>ライトの温度やが一番の光センサーをサポートしています x と y です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

[**SensorConnectionType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002)

[SensorsCxSensorCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensorcreate)

[センサーのプロパティ](sensor-properties2.md)

[センサーの種類の Guid](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)

 

 







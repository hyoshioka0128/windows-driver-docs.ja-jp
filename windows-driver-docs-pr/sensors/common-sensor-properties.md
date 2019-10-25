---
title: センサーの共通プロパティ
description: このトピックでは、すべてのセンサーに共通のセンサープロパティについて説明します。
ms.assetid: 3E4DD221-BA8E-446E-BA7A-EF84DFED332F
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 654eac3d8f9e93c8d613bfd69a0304f8c3a97199
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842528"
---
# <a name="common-sensor-properties"></a>センサーの共通プロパティ


このトピックでは、すべてのセンサーに共通のセンサープロパティについて説明します。

次の表は、共通プロパティを示しています。 [型] 列に表示される型の詳細については、「 [Propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

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
<th>プロパティキー</th>
<th>タスクバーの検索ボックスに</th>
<th>アクセス (R/O、R/W)</th>
<th>必須/オプション</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_Sensor_Type</p></td>
<td><p>VT_CLSID</p></td>
<td><p>R/O</p></td>
<td><p>必須かどうか</p></td>
<td><p>センサーの種類。 GUID は、Windows センサーと同じ形式 (たとえば、SENSOR_TYPE_ACCELEROMETER_3D) で構成されます。 センサーの種類の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants" data-raw-source="[Sensor type GUIDs](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)">センサーの種類の guid</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_Sensor_State</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必須かどうか</p></td>
<td><p>センサーの状態。 センサーの状態の詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-sensor_state" data-raw-source="[&lt;strong&gt;SENSOR_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-sensor_state)"><strong>SENSOR_STATE</strong></a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_MinimumDataInterval_Ms</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必須かどうか</p></td>
<td><p>センサーデータレポートを生成するためにハードウェアがサポートする最小時間間隔 (ミリ秒単位)。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_Sensor_MaximumDataFieldSize_Bytes</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必須かどうか</p></td>
<td><p>ReadFile 呼び出しで返される最大サイズ。 ReadFile 呼び出しを使用すると、ネイティブ API は任意のデータフィールドを保持するバッファーを割り当てることができます。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_Power_Milliwatts</p></td>
<td><p>VT_R4</p></td>
<td><p>R/O</p></td>
<td><p>オプション</p></td>
<td><p>センサーの電力がミリ秒単位で表されます。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorHistory_MaxSize_Bytes</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>オプション</p>
<p>ただし、センサーで履歴がサポートされている場合は必須です。</p></td>
<td><p>センサー履歴データの最大サイズ (バイト単位)。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorHistory_Interval_Ms</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>オプション</p>
<p>ただし、センサーで履歴がサポートされている場合は必須です。</p></td>
<td><p>センサー履歴のサンプリング間隔 (ミリ秒単位)。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorHistory_MaximumRecordSize_Bytes</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>オプション</p>
<p>ただし、センサーで履歴がサポートされている場合は必須です。</p></td>
<td><p>バイト単位で表現された最大レコードサイズ。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_FifoReservedSize_Samples</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>オプション</p>
<p>ただし、センサーでバッチ処理がサポートされている場合は必須です。</p></td>
<td><p>バッチの先入れ先出し (FIFO) バッファーで、このセンサー用に予約されているイベントの数。 これにより、イベントの最小数が保証されます。 この値が0の場合、センサーがバッチ処理を実行する保証はありません。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_Sensor_FifoMaxSize_Samples</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>オプション</p>
<p>ただし、センサーでバッチ処理がサポートされている場合は必須です。</p></td>
<td><p>FIFO でバッチ処理できるイベントの最大数。 この値が0の場合、バッチ処理はセンサーでサポートされていません。 バッチ FIFO は複数のセンサーで共有できるため、実際のイベント数はこの数値よりも小さくなることがあります。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_WakeCapable</p></td>
<td><p>VT_BOOL</p></td>
<td><p>R/O</p></td>
<td><p>オプション</p>
<p>ただし、センサーでバッチ処理がサポートされている場合は必須です。</p></td>
<td><p>センサーがウェイクアップに対応しているかどうかを示します。</p>
<p>センサーでセンサーバッチ処理がサポートされている場合、センサーがいっぱいになったときにアプリケーションプロセッサをスリープ解除できる場合は、これを VARIANT_TRUE に設定する必要があります。 センサーがアプリケーションプロセッサをスリープ解除できない場合は、値を VARIANT_FALSE に設定する必要があります。 この場合、このプロパティの状態は、接続されたスタンバイからスリープ解除するセンサーの機能を示します。</p>
<p>センサーが SX からのシステムのスリープ解除をサポートしている場合、このプロパティを VARIANT_TRUE に設定する必要があります。また、SX からのウェイクアップをサポートしていない場合、このプロパティは VARIANT_FALSE に設定する必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idnotespanspan-idnotespanspan-idnotespannote"></a><span id="Note"></span><span id="note"></span><span id="NOTE"></span>付箋


データのバッチ処理をサポートするセンサードライバーは、次の一般的なセンサーのプロパティを報告する必要があります。

-   PKEY\_センサー\_FifoReservedSize\_サンプル

-   PKEY\_センサー\_Fi@ Maxsize\_サンプル

-   PKEY\_センサー\_WakeCapable

Windows 10 バージョン1511以降では、HID センサークラスドライバーを使用してデータのバッチ処理を実装できるようになりました。 詳細については、「[センサーバッチ処理コントロール](sensor-batching-for-power-saving-.md)」を参照してください。

データのバッチ処理に関連するコールバック関数の詳細については、「 [Evtsensorsetbatchlatency](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) 」を参照してください。

センサーが SX 状態から CPU とオペレーティングシステムをウェイクアップできる追加機能により、PKEY\_センサー\_WakeCapable は、PnP ドライバーストアから照会してセンサーが可能かどうかを調べることができる列挙プロパティとしても使用されます。接続されたスタンバイからシステムをウェイクアップするだけでなく、SX からシステムをウェイクアップします。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


クライアントドライバーが次のプロパティを報告する場合、クライアントドライバーは**CollectionsListGetMarshalledSize**ではなく**CollectionsListGetMarshalledSizeWithoutSerialization**を使用する必要があります。

-   PKEY\_SensorHistory\_MaxSize\_Bytes

-   PKEY\_SensorHistory\_MaximumRecordSize\_Bytes

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[EvtSensorSetBatchLatency](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

[センサーのプロパティ](sensor-properties2.md)

[**センサーの\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-sensor_state)

[センサーの種類の Guid](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)

 

 







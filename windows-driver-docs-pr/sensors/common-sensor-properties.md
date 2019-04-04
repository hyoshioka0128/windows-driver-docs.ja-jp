---
title: センサーの共通プロパティ
description: このトピックでは、すべてのセンサーの一般的なセンサー プロパティについて説明します。
ms.assetid: 3E4DD221-BA8E-446E-BA7A-EF84DFED332F
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7aa167e2b04935467d8638ea909372dc4847624a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536541"
---
# <a name="common-sensor-properties"></a>センサーの共通プロパティ


このトピックでは、すべてのセンサーの一般的なセンサー プロパティについて説明します。

次の表では、一般的なプロパティを示します。 型の列に示すように種類の詳細については、[PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)を参照してください。

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
<th>プロパティのキー</th>
<th>種類</th>
<th>アクセス (R/O、読み取り/書き込み)</th>
<th>必須/オプション</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_Sensor_Type</p></td>
<td><p>VT_CLSID</p></td>
<td><p>R/O</p></td>
<td><p>必須</p></td>
<td><p>センサーの種類。 GUID は、Windows センサー (SENSOR_TYPE_ACCELEROMETER_3D など) と同じ形式で構成されます。 センサーの種類の詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/dn946707" data-raw-source="[Sensor type GUIDs](https://msdn.microsoft.com/library/windows/hardware/dn946707)">センサーの種類の Guid</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_Sensor_State</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必須</p></td>
<td><p>センサーの状態。 センサーの状態の詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/dn946703" data-raw-source="[&lt;strong&gt;SENSOR_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn946703)"> <strong>SENSOR_STATE</strong></a>を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_MinimumDataInterval_Ms</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必須</p></td>
<td><p>センサー データのレポート生成用ハードウェアをサポートする最小時間 (ミリ秒単位) 間隔。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_Sensor_MaximumDataFieldSize_Bytes</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必須</p></td>
<td><p>最大サイズは、ReadFile 呼び出しで返されます。 ReadFile 呼び出しには、ネイティブの API を任意のデータ フィールドを保持するバッファーを割り当てることができます。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_Power_Milliwatts</p></td>
<td><p>VT_R4</p></td>
<td><p>R/O</p></td>
<td><p>省略可能</p></td>
<td><p>センサーの電源をミリ ワットで表されます。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorHistory_MaxSize_Bytes</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>省略可能</p>
<p>必要です、センサーは、履歴をサポートしている場合。</p></td>
<td><p>センサー履歴データ、バイト単位の最大サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorHistory_Interval_Ms</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>省略可能</p>
<p>必要です、センサーは、履歴をサポートしている場合。</p></td>
<td><p>センサー履歴のサンプリング間隔は、ミリ秒単位で表されます。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorHistory_MaximumRecordSize_Bytes</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>省略可能</p>
<p>必要です、センサーは、履歴をサポートしている場合。</p></td>
<td><p>バイト単位で表される最大レコード サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_FifoReservedSize_Samples</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>省略可能</p>
<p>必要です、センサーは、バッチ処理をサポートしている場合。</p></td>
<td><p>このセンサーは、バッチの最初先出し (FIFO) のバッファー内の予約済みのイベントの数。 これにより、イベントの最小数。 この値が 0 の場合、センサーがバッチ処理を実行することの保証はありません。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_Sensor_FifoMaxSize_Samples</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>省略可能</p>
<p>必要です、センサーは、バッチ処理をサポートしている場合。</p></td>
<td><p>でしたが、FIFO でバッチ処理対象のイベントの最大数。 この値が 0 の場合、バッチ処理は、センサーによってサポートされません。 イベントの実際の数は、以降の複数のセンサーで共有できる FIFO、バッチこの数より小さくする可能性があります。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_WakeCapable</p></td>
<td><p>VT_BOOL</p></td>
<td><p>R/O</p></td>
<td><p>省略可能</p>
<p>必要です、センサーは、バッチ処理をサポートしている場合。</p></td>
<td><p>センサーはウェイク アップに対応しているかどうかを示します。</p>
<p>センサーでは、センサーがバッチ処理をサポートするときに、FIFO がいっぱいのとき、センサーが、アプリケーションのプロセッサをスリープ解除できる場合これは、VARIANT_TRUE に設定する必要があります。 値は、センサーは、アプリケーションのプロセッサをスリープ解除できない場合は VARIANT_FALSE に設定する必要があります。 この場合、このプロパティの状態は、コネクト スタンバイから復帰するセンサーの機能を示します。</p>
<p>センサー SX からシステムをスリープ解除をサポートするには、このプロパティは、VARIANT_TRUE に設定する必要があり、サポートしていないかどうかは、SX から復帰する場合、このプロパティが VARIANT_FALSE に設定する必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idnotespanspan-idnotespanspan-idnotespannote"></a><span id="Note"></span><span id="note"></span><span id="NOTE"></span>注


データのバッチ処理をサポートするセンサー ドライバーでは、次の一般的なセンサー プロパティを報告する必要があります。

-   鍵\_センサー\_FifoReservedSize\_サンプル

-   鍵\_センサー\_FifoMaxSize\_サンプル

-   鍵\_センサー\_WakeCapable

Windows 10、バージョン 1511 以降でサポートが HID センサー クラス ドライバーを使用してデータのバッチ処理を実装するために使用できます。 これについては、[センサーのバッチ処理コントロール](sensor-batching-for-power-saving-.md)を参照してください。

参照してください[EvtSensorSetBatchLatency](https://msdn.microsoft.com/library/windows/hardware/mt219125)については、コールバック関数に関連するデータのバッチ処理します。

CPU と、鍵の SX 状態からのオペレーティング システムをスリープ解除する、センサーの追加機能と共に\_センサー\_WakeCapable がセンサーのかどうかを検索する PnP ドライバー ストアからクエリを実行できる列挙型のプロパティとしても使用されますコネクト スタンバイからシステムをスリープ解除だけでなく、SX からシステムをスリープ解除できること。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


クライアント ドライバーでは、次のプロパティをレポート、クライアント ドライバーで使用する必要があります**CollectionsListGetMarshalledSizeWithoutSerialization**の代わりに**CollectionsListGetMarshalledSize**:

-   鍵\_SensorHistory\_MaxSize\_バイト

-   鍵\_SensorHistory\_MaximumRecordSize\_バイト

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[EvtSensorSetBatchLatency](https://msdn.microsoft.com/library/windows/hardware/mt219125)

[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

[センサーのプロパティ](sensor-properties2.md)

[**センサー\_状態**](https://msdn.microsoft.com/library/windows/hardware/dn946703)

[センサーの種類の Guid](https://msdn.microsoft.com/library/windows/hardware/dn946707)

 

 







---
title: コレクション リスト レガシ ヘルパー
description: コレクションリストのレガシヘルパー関数は、センサー\_コレクション\_リスト構造体と対話するために v2 センサードライバーによって使用されます。
ms.assetid: AD5AB3EE-5AD7-4576-8E8E-3FEA08930DD7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 60a02bdabb936e888a00a62258823913f18deebc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842532"
---
# <a name="collection-list-legacy-helpers"></a>コレクション リスト レガシ ヘルパー


コレクションリストのレガシヘルパー関数は、[**センサー\_コレクション\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体と対話するために v2 センサードライバーによって使用されます。

ヘルパー関数は、センサーデバイスドライバーソフトウェアインターフェイス (DDSI) と共に使用されます。

**注:** これらの従来のコレクションリストヘルパー関数は、アーキテクチャに固有のものです。 したがって、独自のコレクションリストヘルパー関数を実装する場合、センサードライバーは、プロセスの境界を越えてデータを転送するためにそれらを使用することはできません。

**CollectionsListGetMarshalledSize**

センサー DDSI による使用量

-   PKEY\_センサー\_MaximumDataFieldSize\_Bytes プロパティの値を設定します。

-   [EvtSensorGetProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)から*pSize*値を返します。

-   [*EvtSensorGetDataFieldProperties*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)から*pSize*値を返します。

-   [*Evtsensorgetdatathresholds*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)値から*pSize*値を返します。

コメント

-   *PSize*メンバーの詳細については、「[**センサー\_COLLECTION\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 」を参照してください。

-   詳細については、「[一般的なセンサーのプロパティ](common-sensor-properties.md)」も参照してください。

**CollectionsListCopyAndMarshall**

センサー DDSI による使用量

-   [*EvtSensorGetProperties*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) のコレクションリストを設定します。

-   [*EvtSensorGetDataFieldProperties*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) のコレクションリストを設定します。

-   [ *Evtsensorgetdatathresholds 値*のコレクションリストを設定します](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

コメント

-   詳細については、「[**センサー\_コレクション」\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)を参照してください。

**CollectionsListMarshall**

センサー DDSI による使用量

-   コレクションリストへのポインターを返します。

コメント

-   詳細については、「[**センサー\_コレクション」\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)を参照してください。

**CollectionsListGetMarshalledSizeWithoutSerialization**

センサー DDSI による使用量

-   **PKEY\_SensorHistory\_MaxSize\_Bytes**プロパティを報告します。

-   **PKEY\_SensorHistory\_MaximumRecordSize\_Bytes**プロパティを報告します。

コメント

-   詳細については、「[センサーの共通プロパティ](common-sensor-properties.md)」を参照してください。

**CollectionsListUpdateMarshalledPointer**

センサー DDSI による使用量

-   [*Evtsensorsetdatathresholds 値*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)を使用して、センサードライバーにバッファーを渡します。

-   [*EvtSensorDeviceIoControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)を使用して、ドライバーにバッファーを渡します。

コメント

-   詳細については、「[**センサー\_コレクション」\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)を参照してください。

## <a name="requirements"></a>要件

|                          |                        |
|--------------------------|------------------------|
| サポートされている最小のクライアント | Windows 8.1            |
| サポートされている最小のサーバー | Windows Server 2012 R2 |
| Header                   | Sensorsutils         |

 

## <a name="related-topics"></a>関連トピック


[マーシャリングヘルパー関数](marshalling-helper-functions.md)

 

 







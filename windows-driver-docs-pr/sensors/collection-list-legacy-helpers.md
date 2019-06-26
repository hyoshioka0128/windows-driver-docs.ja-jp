---
title: コレクション リスト レガシ ヘルパー
description: コレクションの一覧の従来のヘルパー関数は、センサーを操作する v2 センサー ドライバーによって使用されて\_コレクション\_リストの構造体。
ms.assetid: AD5AB3EE-5AD7-4576-8E8E-3FEA08930DD7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 600977b9c952d06d3590e253f1388903a1a0d712
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354905"
---
# <a name="collection-list-legacy-helpers"></a>コレクション リスト レガシ ヘルパー


コレクションの一覧の従来のヘルパー関数は、のやり取りの v2 センサー ドライバーによって使用されて[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体。

ヘルパー関数は、センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) と共に使用されます。

**注:** これらのレガシ コレクション リスト ヘルパー関数は、アーキテクチャ固有です。 したがって、独自のコレクション一覧ヘルパー関数を実装する場合センサー ドライバーする必要があるために使用しないプロセスの境界を越えてデータを転送します。

**CollectionsListGetMarshalledSize**

センサー DDSI による使用量

-   鍵の値を設定\_センサー\_MaximumDataFieldSize\_バイト プロパティ。

-   返します、 *pSize*値から[EvtSensorGetProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)します。

-   返します、 *pSize*値から[ *EvtSensorGetDataFieldProperties*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)します。

-   返します、 *pSize*値から[ *EvtSensorGetDataThresholds*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)します。

コメント

-   参照してください[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)の詳細については、 *pSize*メンバー。

-   またを参照してください[センサーの共通プロパティ](common-sensor-properties.md)詳細についてはします。

**CollectionsListCopyAndMarshall**

センサー DDSI による使用量

-   コレクションの一覧を設定します[ *EvtSensorGetProperties。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)

-   コレクションの一覧を設定します[ *EvtSensorGetDataFieldProperties。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)

-   コレクションの一覧を設定します[ *EvtSensorGetDataThresholds。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)

コメント

-   参照してください[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)詳細についてはします。

**CollectionsListMarshall**

センサー DDSI による使用量

-   コレクションの一覧へのポインターを返します。

コメント

-   参照してください[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)詳細についてはします。

**CollectionsListGetMarshalledSizeWithoutSerialization**

センサー DDSI による使用量

-   レポート、**鍵\_SensorHistory\_MaxSize\_バイト**プロパティ。

-   レポート、**鍵\_SensorHistory\_MaximumRecordSize\_バイト**プロパティ。

コメント

-   参照してください[センサーの共通プロパティ](common-sensor-properties.md)詳細についてはします。

**CollectionsListUpdateMarshalledPointer**

センサー DDSI による使用量

-   センサーのドライバーを使用するバッファーを渡します[ *EvtSensorSetDataThresholds*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)します。

-   使用して、ドライバーにバッファーを渡す[ *EvtSensorDeviceIoControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)します。

コメント

-   参照してください[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)詳細についてはします。

## <a name="requirements"></a>要件

|                          |                        |
|--------------------------|------------------------|
| サポートされている最小のクライアント | Windows 8.1            |
| サポートされている最小のサーバー | Windows Server 2012 R2 |
| Header                   | Sensorsutils.h         |

 

## <a name="related-topics"></a>関連トピック


[ヘルパー関数をマーシャ リング](marshalling-helper-functions.md)

 

 







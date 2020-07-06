---
title: コレクション リスト レガシ ヘルパー
description: コレクションリストのレガシヘルパー関数は、センサーコレクションのリスト構造を操作するために v2 センサードライバーによって使用され \_ \_ ます。
ms.assetid: AD5AB3EE-5AD7-4576-8E8E-3FEA08930DD7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 20dfe9f5844bc9f2347da9fe40be306536b341d7
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967913"
---
# <a name="collection-list-legacy-helpers"></a>コレクション リスト レガシ ヘルパー


コレクションリストのレガシヘルパー関数は、[**センサー \_ コレクションの \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)構造を操作するために v2 センサードライバーによって使用されます。

ヘルパー関数は、センサーデバイスドライバーソフトウェアインターフェイス (DDSI) と共に使用されます。

**注:** これらの従来のコレクションリストヘルパー関数は、アーキテクチャに固有のものです。 したがって、独自のコレクションリストヘルパー関数を実装する場合、センサードライバーは、プロセスの境界を越えてデータを転送するためにそれらを使用することはできません。

**CollectionsListGetMarshalledSize**

センサー DDSI による使用量

-   PKEY \_ センサーの \_ maximumdatafieldsize \_ (バイト数) プロパティの値を設定します。

-   [EvtSensorGetProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)から*pSize*値を返します。

-   [*EvtSensorGetDataFieldProperties*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)から*pSize*値を返します。

-   [*Evtsensorgetdatathresholds*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)値から*pSize*値を返します。

コメント

-   *PSize*メンバーの詳細については、「[**センサー \_ コレクションの \_ 一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)」を参照してください。

-   詳細については、「[一般的なセンサーのプロパティ](common-sensor-properties.md)」も参照してください。

**CollectionsListCopyAndMarshall**

センサー DDSI による使用量

-   EvtSensorGetProperties のコレクションリストを設定します。 [ *EvtSensorGetProperties*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

-   EvtSensorGetDataFieldProperties のコレクションリストを設定します。 [ *EvtSensorGetDataFieldProperties*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

-   [ *Evtsensorgetdatathresholds 値*のコレクションリストを設定します](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

コメント

-   詳細については、「[**センサー \_ コレクションの \_ 一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)」を参照してください。

**CollectionsListMarshall**

センサー DDSI による使用量

-   コレクションリストへのポインターを返します。

コメント

-   詳細については、「[**センサー \_ コレクションの \_ 一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)」を参照してください。

**CollectionsListGetMarshalledSizeWithoutSerialization**

センサー DDSI による使用量

-   **PKEY \_ sensorhistory \_ MaxSize \_ Bytes**プロパティを報告します。

-   **PKEY \_ sensorhistory \_ maximumrecordsize \_ Bytes**プロパティを報告します。

コメント

-   詳細については、「[センサーの共通プロパティ](common-sensor-properties.md)」を参照してください。

**CollectionsListUpdateMarshalledPointer**

センサー DDSI による使用量

-   [*Evtsensorsetdatathresholds 値*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)を使用して、センサードライバーにバッファーを渡します。

-   [*EvtSensorDeviceIoControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)を使用して、ドライバーにバッファーを渡します。

コメント

-   詳細については、「[**センサー \_ コレクションの \_ 一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)」を参照してください。

## <a name="requirements"></a>要件

**サポートされている最低限のクライアント**: Windows 8.1

**サポートされている最小サーバー**: Windows Server 2012 R2

**ヘッダー**: Sensorsutils


 

## <a name="related-topics"></a>関連トピック


[マーシャリング ヘルパーの関数](marshalling-helper-functions.md)

 

 







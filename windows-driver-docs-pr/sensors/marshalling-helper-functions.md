---
title: マーシャリング ヘルパーの関数
description: このトピックでは、sensorsutils.h ヘッダー ファイルのマーシャ リングのヘルパー関数についての情報を提供します。
ms.assetid: AE5C70E4-1971-4BAF-AE7D-315A15F030DD
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1d2af831155fcea2123eaa6221471921d812399a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345112"
---
# <a name="marshalling-helper-functions"></a>マーシャリング ヘルパーの関数


このトピックではマーシャ リングのヘルパー関数について、 *sensorsutils.h*ヘッダー ファイル。

これらのヘルパー関数は、v2 センサー ドライバーによって使用され、センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) と共に使用されます。

マーシャ リングのヘルパー関数を実装する場合の列挙リストを設定するときにヘルパー関数を使用しない必要がありますに注意してください、 [**センサー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_config)構造体、またはレポートを使用してデータを更新、 [ **SensorsCxSensorDataReady** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)関数。

## <a name="in-this-section"></a>このセクションの内容


|トピック|説明|
|--|--|
|[タイム スタンプ ヘルパー](timestamp-helper.md)|タイム スタンプのヘルパー関数は v2 センサー ドライバーによって使用され、センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) と共に使用します。|
|[PropVariant ヘルパー](propvariant-helpers.md)|PropVariant のヘルパー関数が操作に v2 センサー ドライバーによって使用される、 [PROPVARIANT](https://msdn.microsoft.com/library/windows/desktop/aa380072.aspx)センサーに関連付けられている構造体。|
|[コレクションの一覧のヘルパー](collection-list-helpers.md)|コレクションの一覧のヘルパー関数が操作するため v2 センサー ドライバーによって使用される[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体。|
|[コレクションの一覧のシリアル化ヘルパー](collection-list-serialization-helpers.md)|コレクション リストのシリアル化ヘルパー関数がでシリアル化関連の操作を実行するため、v2 センサー ドライバーで使用される[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体。|
|[コレクションの一覧のレガシ ヘルパー](collection-list-legacy-helpers.md)|コレクションの一覧の従来のヘルパー関数は、のやり取りの v2 センサー ドライバーによって使用されて[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体。|

 

## <a name="requirements"></a>要件


**ヘッダー:** Sensorsutils.h

 

 






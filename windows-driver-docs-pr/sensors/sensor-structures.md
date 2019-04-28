---
title: センサーの構造体
description: センサーの構造体
ms.assetid: 94194998-8A56-48D3-9053-007526BF0ED2
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62e6bbf7173d4e813fa73cc0c1ca34246befaac9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368806"
---
# <a name="sensor-structures"></a>センサーの構造体

このセクションには、さまざまなプロパティとセンサーの機能へのアクセスを提供するセンサー構造に関する情報が含まれています。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|---|---|
|[SENSOR_VALUE_PAIR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_value_pair)|この構造は、プロパティのキーにそれぞれのキーを表すデータ センサーのプロパティ セクションに記載ペア。|
|[SENSOR_COLLECTION_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)|この構造体には、各センサーのすべての SENSOR_VALUE_PAIR 構造の一覧が含まれています。|
|[SENSOR_PROPERTY_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)|この構造体には、各センサーのすべての SENSOR_VALUE_PAIR 構造の一覧が含まれています。|
|[SENSOR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_config)|この構造体には、センサー ドライバーは、各センサーに関するクラスの拡張機能に渡される情報が含まれています。|
|[SENSOR_CONTROLLER_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)|この構造体には、ドライバによって実装して呼び出すクラスの拡張機能に渡す必要があるコールバック関数へのポインターが含まれています。|
|SENSOR_DATA|この構造体は、センサーに固有のデータ型を定義するその他のセンサーを使用する基本データ型を定義します。|
|SENSOR_DEVICE_CAPS|この構造体には、センサー コンポーネントの機能について説明します。|
|SENSOR_DATA_HEADER|この構造体には、センサーの読み取りに関する情報が含まれています。|
|VEC3D|この構造体は 3D の位置データの 1 つのデータ ポイントを保持します。|
|四元数|この構造体は、単純な 3-D 回転の操作に使用される 4 次元ベクトルを表すために使用されます。|
|MATRIX3X3|この構造体は、汎用の 3 x 3 行列を表すために使用されます。|







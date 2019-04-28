---
title: センサー データ フィールド
description: センサー ドライバーでは、センサー ドライバーに関する情報を取得する ReadFile 関数を使用して、アプリケーションが読み取ることができるデータ フィールドを設定します。
ms.assetid: E430AC59-34AC-4F8E-9A42-350C7A42BBA8
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ac26975bef9eb3025021585d5d9902d8b646cd8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368870"
---
# <a name="sensor-data-fields"></a>センサー データ フィールド

*センサー データ フィールド*センサーを提供する情報の特定の種類を表します。 格納される値といいますデータをレポートするときに、*データ フィールド*します。 関連するデータ フィールドのコレクションを構成、*データ レポート*します。 SENSOR_COLLECTION_LIST 構造内でデータ レポートをまとめてパッケージ化されます。 各データ レポートには、少なくとも 1 つの有効なデータ フィールドとデータのレポートの作成時に識別するタイムスタンプを含める必要があります。 タイムスタンプは、PKEY_SensorData_Timestamp プロパティのキーによって表されます。 データ フィールドには、x、y、z の高速化値、加速度計があります。 各データ フィールドがで識別される、 **PROPERTYKEY**定数。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|---|---|
|[一般的なデータ フィールド](common-data-fields.md)|このトピックでは、すべてのセンサーに固有のデータ フィールドに含まれている共通のデータ フィールドを示します。|
|[加速度計データ フィールド](accelerometer-data-fields.md)|このトピックでは、加速度計に固有のデータ フィールドの詳細についての情報を提供します。|
|[線形の加速度計データ フィールド](linear-accelerometer-data-fields.md)|このトピックでは、線形の加速度計に固有のデータ フィールドの詳細についての情報を提供します。|
|[磁力計データ フィールド](magnetometer-data-fields.md)|このトピックでは、磁力計に固有のデータ フィールドの詳細についての情報を提供します。|
|[Geomagnetic 向き](geomagnetic-orientation.md)|> このトピックでは、geomagnetic 方向センサーに固有のデータ フィールドに関する情報を提供します。|
|[重力ベクター データ フィールド](gravity-vector-data-fields.md)|> このトピックでは、重力ベクトルに固有のデータ フィールドに関する情報を提供します。|
|[データ フィールドのジャイロスコープなどがあります。](gyroscope-data-fields.md)|このトピックでは、ジャイロスコープなどがありますに固有のデータ フィールドの詳細についての情報を提供します。|
|[光センサーのデータ フィールド](light-sensor-data-fields.md)|このトピックでは、光センサーに固有のデータ フィールドの詳細についての情報を提供します。|
|[方向センサーのデータ フィールド](device-orientation-sensor-data-fields.md)|このトピックでは、デバイスの方向センサーに固有のデータ フィールドの詳細についての情報を提供します。|
|[近接センサーのデータ フィールド](proximity-sensor-data-fields.md)|このトピックでは、近接センサーに固有のデータ フィールドに関する情報を提供します。|
|[バロメーターになるデータ フィールド](barometer-sensor-data-fields.md)|このトピックでは、バロメーター センサーに固有のデータ フィールドの詳細についての情報を提供します。|
|[シンプルなデバイスの向きのセンサー データ フィールド](simple-device-orientation-sensor-data-fields.md)|このトピックでは、単純なデバイスの方向センサーに固有のデータ フィールドの詳細についての情報を提供します。|
|[アクティビティ検出のセンサー データのフィールド](activity-detection-sensor-data-fields.md)|このトピックでは、アクティビティの検出のセンサーに固有のデータ フィールドの詳細についての情報を提供します。|
|[データ フィールドの歩数計](pedometer-data-fields.md)|このトピックでは、歩数計に固有のデータ フィールドの詳細についての情報を提供します。|
|[相対的な方向センサーのデータ フィールド](relative-orientation-data-fields.md)|このトピックでは、相対的な方向センサーに固有のデータ フィールドの詳細についての情報を提供します。|
|[カスタムのセンサー データ フィールド](custom-sensor-data-fields.md)|このトピックでは、カスタム センサーで使用できるデータ フィールドに関する情報を提供します。|

 

 

 






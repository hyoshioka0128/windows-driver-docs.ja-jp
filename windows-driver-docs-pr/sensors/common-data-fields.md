---
title: 共通データ フィールド
description: このトピックでは、センサー固有のすべてのデータフィールドに含まれる共通データフィールドについて説明します。
ms.assetid: 5F9F7987-E898-404A-96F9-F5CF88F01393
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ebbd5e0c80f0901cef5afa7d5143676eebdd920a
ms.sourcegitcommit: 36b7db40d5a91d8726feb2e2d9d4ece1fb484051
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72591017"
---
# <a name="sensor-data-fields"></a>センサー データ フィールド

*センサーデータフィールド*は、センサーが提供できる特定の種類の情報を表します。 データをレポートする場合、値は*データフィールド*に含まれると言われます。 関連するデータフィールドのコレクションは、*データレポート*を構成します。 データレポートは、SENSOR_COLLECTION_LIST 構造内にまとめてパッケージ化されます。 各データレポートには、少なくとも1つの有効なデータフィールドと、データレポートが作成された日時を示すタイムスタンプが含まれている必要があります。 タイムスタンプは、PKEY_SensorData_Timestamp プロパティキーによって表されます。 データフィールドの例としては、加速度計の x、y、z 加速度の値などがあります。 各データフィールドは**Propertykey**定数によって識別されます。

## <a name="common-data-fields"></a>共通データ フィールド

以下のフィールドの種類は、センサー固有のすべてのデータフィールドに含まれています。

クライアントは、ReadFile 関数を使用して、これらのデータフィールドから情報を取得できます。

[型] 列に表示される型の詳細については、「 [Propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|タスクバーの検索ボックスに|必須/オプション|説明|
| --- | --- | --- | --- |
|PKEY_SensorData_Timestamp|VT_FILETIME|必須かどうか|ドライバーによって計算されたファイルの時刻 (UTC 形式)。 クラス拡張 (CX) には、タイマー刻みをブートから FILETIME に変換するヘルパー関数が用意されています。これにより、リモートシステムがシステムクロックに同期する必要がなくなります。|

## <a name="related-topics"></a>関連トピック

[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

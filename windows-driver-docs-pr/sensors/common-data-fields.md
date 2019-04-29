---
title: 共通データ フィールド
description: このトピックでは、すべてのセンサーに固有のデータ フィールドに含まれている共通のデータ フィールドを示します。
ms.assetid: 5F9F7987-E898-404A-96F9-F5CF88F01393
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 956333d250f31653da9f9c263fc5abfe5dec5a49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325267"
---
# <a name="common-data-fields"></a>共通データ フィールド


このトピックでは、すべてのセンサーに固有のデータ フィールドに含まれている共通のデータ フィールドを示します。

クライアントは、ReadFile 関数を使用して、これらのデータ フィールドから情報を取得できます。

次の表では、共通のデータ フィールドを示します。

型の列に示すように種類の詳細については、次を参照してください。 [PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|説明|
| --- | --- | --- | --- |
|PKEY_SensorData_Timestamp|VT_FILETIME|必須|ファイルの時刻が UTC 形式で、ドライバーによって計算されます。 クラスの拡張機能 (CX) は、リモート システムは、システム クロックに同期する必要があるないようにの FILETIME をブートからのティックを変換するヘルパー関数を提供します。|

 

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 







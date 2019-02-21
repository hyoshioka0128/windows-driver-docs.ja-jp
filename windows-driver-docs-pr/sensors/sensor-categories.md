---
title: センサーのカテゴリ
description: センサーのカテゴリ
ms.assetid: 609C57BA-1C3E-435B-BAAE-C01C3669D59D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1ef5a02034cbe1b8fa11c7a25321e959efdd72e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536722"
---
# <a name="sensor-categories"></a>センサーのカテゴリ

センサーのカテゴリは、センサー デバイスの広範なクラスを表します。 カテゴリは、グループのセンサーのような種類の情報を提供する可能性が高いまたは何らかの方法で関連するそれ以外の場合をする方法を提供します。 各カテゴリは、GUID 定数で表されます。 さまざまな種類の 2 つのセンサーは、同じカテゴリまたは 2 つの異なるカテゴリに属することができます。 たとえば、加速度計、ジャイロスコープ可能性があります両方分類 GUID_SensorCategory_Motion カテゴリでは、GUID_SensorCategory_Light カテゴリの下に、環境光センサーを分類することが中に。 各センサーのカテゴリは、GUID 定数で表されます。

センサーのカテゴリの Guid が SensorsDef.h で定義されています。

| 名前 | 説明 |
| --- | --- |
| GUID_SensorCategory_All| この GUID は、すべてのセンサーを識別します。 センサー クラスの拡張機能は、以下のカテゴリの 1 つは、ドライバーが明示的に提供しない限り、このカテゴリにセンサーを追加します。 |
| GUID_SensorCategory_Biometric | この GUID は、生体認証センサー カテゴリを識別します。 |
| GUID_SensorCategory_Electrical | この GUID は、電気センサー カテゴリを識別します。 |
| GUID_SensorCategory_Environmental| この GUID は、環境のセンサーのカテゴリを識別します。 |
| GUID_SensorCategory_Light| この GUID は、光センサーのカテゴリを識別します。 |
| GUID_SensorCategory_Location | この GUID は、場所のセンサーのカテゴリを識別します。 |
| GUID_SensorCategory_Mechanical| この GUID は、機械のセンサーのカテゴリを識別します。 |
| GUID_SensorCategory_Motion| この GUID は、モーション センサーのカテゴリを識別します。 |
| GUID_SensorCategory_Orientation | この GUID は、方向センサーのカテゴリを識別します。 |
| GUID_SensorCategory_Other | この GUID は、センサーではサポートされますが、定義済みのカテゴリのいずれかに収まらないのカテゴリを識別します。 |
| GUID_SensorCategory_Scanner| この GUID は、スキャナーのセンサーのカテゴリを識別します。 |
| GUID_SensorCategory_Unsupported| この GUID は、サポートされていないセンサーのカテゴリを識別します。 |


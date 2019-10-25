---
title: コレクション リスト ヘルパー
description: コレクションリストヘルパー関数は、センサー\_コレクション\_リスト構造体を操作するために、v2 センサードライバーによって使用されます。
ms.assetid: 9BE06FA6-A171-4760-9D3E-C0183F3C3EFA
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9455f58104648238b26e0b1cebbd748c4f7de6e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842534"
---
# <a name="collection-list-helpers"></a>コレクション リスト ヘルパー


コレクションリストヘルパー関数は、[**センサー\_コレクション\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体を操作するために、v2 センサードライバーによって使用されます。

ヘルパー関数は、センサーデバイスドライバーソフトウェアインターフェイス (DDSI) と共に使用されます。

**SensorCollectionGetAt**

センサー DDSI による使用量

-   コレクションリストのプロパティキーと PROPVARIANT 関連の属性を取得します。

コメント

-   詳細については、「[**センサー\_コレクション」\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)を参照してください。

-   詳細については、「[**センサー\_値\_のペア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_value_pair)」を参照してください。

**CollectionsListGetFillableCount**

センサー DDSI による使用量

-   バッファーサイズ (バイト単位) を返します。

コメント

-   なし。

**EvaluateActivityThresholds 値**

センサー DDSI による使用量

-   古いデータサンプルと新しいデータサンプルでアクティビティのしきい値を比較し、ブール値を返します。

コメント

-   なし。

**CollectionsListSortSubscribedActivitiesByConfidence**

センサー DDSI による使用量

-   使用可能なアクティビティのコレクションリストを信頼レベルの順に並べ替えます。

コメント

-   なし。

### <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件

|                          |                        |
|--------------------------|------------------------|
| サポートされている最小のクライアント | Windows 8.1            |
| サポートされている最小のサーバー | Windows Server 2012 R2 |
| Header                   | Sensorsutils         |

 

## <a name="related-topics"></a>関連トピック


[マーシャリングヘルパー関数](marshalling-helper-functions.md)

 

 







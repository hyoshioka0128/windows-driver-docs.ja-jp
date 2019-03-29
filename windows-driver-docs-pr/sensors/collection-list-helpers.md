---
title: コレクション リスト ヘルパー
description: コレクションの一覧のヘルパー関数がセンサーを操作するため、v2 センサー ドライバーで使用される\_コレクション\_リストの構造体。
ms.assetid: 9BE06FA6-A171-4760-9D3E-C0183F3C3EFA
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ab9ca2c16d5d79554bb004c382018b71ee5a561f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573498"
---
# <a name="collection-list-helpers"></a>コレクション リスト ヘルパー


コレクションの一覧のヘルパー関数が操作するため v2 センサー ドライバーによって使用される[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体。

ヘルパー関数は、センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) と共に使用されます。

**SensorCollectionGetAt**

センサー DDSI による使用量

-   プロパティのキーとコレクションの一覧の PROPVARIANT 関連の属性を取得します。

コメント

-   参照してください[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)詳細についてはします。

-   参照してください[**センサー\_値\_ペア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_value_pair)詳細についてはします。

**CollectionsListGetFillableCount**

センサー DDSI による使用量

-   バッファーのサイズ (バイト単位) を返します。

コメント

-   なし。

**EvaluateActivityThresholds**

センサー DDSI による使用量

-   新旧のデータのサンプルでは、アクティビティしきい値を比較し、ブール値を返します。

コメント

-   なし。

**CollectionsListSortSubscribedActivitiesByConfidence**

センサー DDSI による使用量

-   信頼レベルの順序で可能なアクティビティの種類、コレクションが一覧表示します。

コメント

-   なし。

### <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件

|                          |                        |
|--------------------------|------------------------|
| サポートされている最小のクライアント | Windows 8.1            |
| サポートされている最小のサーバー | Windows Server 2012 R2 |
| Header                   | Sensorsutils.h         |

 

## <a name="related-topics"></a>関連トピック


[ヘルパー関数をマーシャ リング](marshalling-helper-functions.md)

 

 







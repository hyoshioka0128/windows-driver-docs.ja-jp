---
title: コレクション リスト ヘルパー
description: コレクションリストヘルパー関数は、センサーコレクションのリスト構造を操作するために、v2 センサードライバーによって使用され \_ \_ ます。
ms.assetid: 9BE06FA6-A171-4760-9D3E-C0183F3C3EFA
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 00f28a70c7f41c5466dc13f7e179f0a8086b60a3
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968237"
---
# <a name="collection-list-helpers"></a>コレクション リスト ヘルパー


コレクションリストヘルパー関数は、[**センサー \_ コレクションの \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)構造を操作するために、v2 センサードライバーによって使用されます。

ヘルパー関数は、センサーデバイスドライバーソフトウェアインターフェイス (DDSI) と共に使用されます。

**SensorCollectionGetAt**

センサー DDSI による使用量

-   コレクションリストのプロパティキーと PROPVARIANT 関連の属性を取得します。

コメント

-   詳細については、「[**センサー \_ コレクションの \_ 一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list)」を参照してください。

-   詳細については、「[**センサー \_ 値の \_ ペア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_value_pair)」を参照してください。

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

### <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>必要性

**サポートされている最低限のクライアント**: Windows 8.1

**サポートされている最小サーバー**: Windows Server 2012 R2

**ヘッダー**: Sensorsutils


 

## <a name="related-topics"></a>関連トピック


[マーシャリング ヘルパーの関数](marshalling-helper-functions.md)

 

 







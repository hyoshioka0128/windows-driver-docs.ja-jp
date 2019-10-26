---
title: TTD Range オブジェクト
description: このセクションでは、タイムトラベルデバッグに関連付けられている範囲モデルオブジェクトについて説明します。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ba30a826e774255b8d94a7d3e194b55f1ead35d
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916179"
---
# <a name="ttd-range-objects"></a>TTD Range オブジェクト

## <a name="description"></a>説明

*TTD range*オブジェクトは、トレースの時間範囲に関する情報を提供するために使用されます。 これらは一般に、TTD セッション中の[TTD thread オブジェクト](time-travel-debugging-thread-objects.md)の有効期間を示すために使用されます。

## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| MinPosition | 範囲に関連する最も早い位置を示す[位置オブジェクト](time-travel-debugging-position-objects.md)。 |
| MaxPosition | 範囲に関連する最新の位置を記述する[位置オブジェクト](time-travel-debugging-position-objects.md)。 |


## <a name="example-usage"></a>使用例

*保留中の情報*

## <a name="see-also"></a>参照

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)


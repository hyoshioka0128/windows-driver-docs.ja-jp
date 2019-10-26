---
title: TTD Position オブジェクト
description: ここでは、タイムトラベルデバッグに関連付けられている位置モデルオブジェクトについて説明します。
ms.date: 12/19/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6daeb58ece76fa37453bb0e1aa26002aff8c7e3a
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916181"
---
# <a name="ttd-position-objects"></a>TTD Position オブジェクト

## <a name="description"></a>説明

*位置*オブジェクトは、タイムトラベルトレース内の位置を記述するために使用されます。 通常、position オブジェクトは、コロンで区切られた2つの16進数で表されます。 16進数の最初の数値は*シーケンス*で、2番目の数値は*手順*です。

FFFFFFFFFFFFFFFE の位置: 0トレースの終了を示します。

## <a name="properties"></a>[プロパティ]

| プロパティ | 説明 |
| --- | --- |
| Sequence | 位置に関連するシーケンスポイント。 |
| 手順 | このスレッド内のシーケンスポイントからこの位置までのステップ数。 |

## <a name="methods"></a>メソッド

| メソッド | 説明 |
| --- | --- |
| SeekTo () | 時間はトレース内のこの位置に移動します。 |

## <a name="example-usage"></a>使用例

*保留中の情報*



## <a name="see-also"></a>参照

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

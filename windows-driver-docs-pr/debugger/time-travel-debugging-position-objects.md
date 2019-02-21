---
title: TTD 位置オブジェクト
description: このセクションでは、タイム トラベルのデバッグに関連付けられているオブジェクトの配置モデルについて説明します。
ms.date: 12/19/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b0fc92625a91645eb807b2ebfae44420ca5e089
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550368"
---
# <a name="ttd-position-objects"></a>TTD 位置オブジェクト
## <a name="description"></a>説明
*位置*オブジェクトは、タイム トラベル トレース内の位置を記述に使用されます。 位置オブジェクトは通常、コロンで区切られた 2 つの 16 進数値をについて説明します。 16 進数の 1 つ目は、*シーケンス*、2 つ目は、*手順*します。

FFFFFFFFFFFFFFFE:0 の位置トレースの最後を示します。

## <a name="properties"></a>プロパティ

| プロパティ | 説明 |
| --- | --- |
| Sequence | シーケンス ポイントの位置に関連します。 |
| 手順 | この位置を取得するには、このスレッド内のシーケンス ポイントからのステップの数。 |

## <a name="methods"></a>メソッド

| メソッド | 説明 |
| --- | --- |
| SeekTo() | 時間は、トレース内のこの位置に移動します。 |

## <a name="example-usage"></a>使用例
*保留中の情報*



## <a name="see-also"></a>参照

[タイム トラベル デバッグ - オブジェクトのタイム トラベルのデバッグの概要](time-travel-debugging-object-model.md)

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---



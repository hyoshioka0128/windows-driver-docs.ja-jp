---
title: TTD Exception オブジェクト
description: このセクションでは、タイムトラベルデバッグに関連付けられている例外モデルオブジェクトについて説明します。
ms.date: 09/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7537ef96faf739c3ebf6d8e7b269e7602e3cc9a
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916215"
---
# <a name="ttd-exception-objects"></a>TTD Exception オブジェクト

## <a name="description"></a>説明

*TTD Exception*オブジェクトは、トレースセッション中に発生した例外に関する情報を提供するために使用されます。


## <a name="properties"></a>[プロパティ]

| プロパティ | 説明 |
| --- | --- |
| タスクバーの検索ボックスに | 例外の種類を記述します。 指定できる値は、"Software" と "Hardware" です。 |
| ProgramCounter | 例外がスローされた命令。  |
| コード | 例外のコード。  |
| フラグ | 例外フラグ。 |
| RecordAddress | メモリ内では、例外のレコードを見つけることができます。  |

## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| 位置 | 例外が発生した位置を示す[位置オブジェクト](time-travel-debugging-position-objects.md)。 |

## <a name="example-usage"></a>使用例

*保留中の情報*

## <a name="see-also"></a>参照

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

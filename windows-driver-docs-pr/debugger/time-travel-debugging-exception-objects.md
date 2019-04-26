---
title: TTD 例外オブジェクト
description: このセクションでは、タイム トラベルのデバッグに関連付けられている例外モデル オブジェクトについて説明します。
ms.date: 09/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1930ad42eda48937c3bf83393a7ff4b621d84246
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342038"
---
# <a name="ttd-exception-objects"></a>TTD 例外オブジェクト
## <a name="description"></a>説明
*TTD 例外*オブジェクトを使用してトレース セッション中に発生した例外に関する情報を提供します。


## <a name="properties"></a>プロパティ

| プロパティ | 説明 |
| --- | --- |
| 種類 | 例外の種類について説明します。 使用可能な値は、「ソフトウェア」と「ハードウェア」です。 |
| ProgramCounter | 例外がスローされた命令。  |
| コード | 例外のコードです。  |
| フラグ | 例外フラグ。 |
| RecordAddress | メモリ内では、例外のレコードを検索できます。  |

## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| 位置 | A[位置オブジェクト](time-travel-debugging-position-objects.md)例外が発生した位置をについて説明します。 |

## <a name="example-usage"></a>使用例

*保留中の情報*



## <a name="see-also"></a>関連項目

[タイム トラベル デバッグ - オブジェクトのタイム トラベルのデバッグの概要](time-travel-debugging-object-model.md)

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---



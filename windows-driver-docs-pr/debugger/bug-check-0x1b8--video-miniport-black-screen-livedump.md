---
title: バグチェック 0x1B8 VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP
description: VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP バグチェックの値は0x000001B8 です。 これは、ユーザーが黒い画面のシナリオでミニポートライブダンプを開始したことを示します。
keywords:
- バグチェック 0x1B8 VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP
- VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP
ms.date: 02/20/2020
topic_type:
- apiref
api_name:
- VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: db47e16744f50163f04b7bb1e74c85149271a146
ms.sourcegitcommit: e018ef208a38bc871b25d9fb72c2501fe4a5f965
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77477151"
---
# <a name="bug-check-0x1b8-video_miniport_black_screen_livedump"></a>バグチェック 0x1B8: ビデオ\_ミニポート\_黒い\_画面\_LIVEDUMP

ビデオ\_ミニポート\_黒い\_画面\_LIVEDUMP バグチェックの値が0x000001B8 です。 これは、ユーザーが黒い画面のシナリオでミニポートライブダンプを開始したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="video_miniport_black_screen_livedump-parameters"></a>ビデオ\_ミニポート\_黒い\_画面\_LIVEDUMP Parameters

|パラメーター|説明|
|--- |--- |
|1| ミニポート黒い画面ライブダンプをトリガーしたソース。下に一覧表示されます。|
|2| 予約済み。 |
|3| 予約済み。 |
|4| 予約済み。 |

**ソース値**

0x1: 黒いスクリーンホットキーが生成されたミニポート黒い画面ライブダンプ

0x2: ボリュームコンボキーによって生成されたミニポート黒い画面ライブダンプ

0x4: 内部で生成されたミニポート黒い画面ライブダンプ

0x8: 長電力ボタンホールド (LPBH) によって生成されたミニポート黒い画面ライブダンプ

## <a name="cause"></a>原因

ブラックスクリーンのシナリオでユーザーが開始したミニポートライブダンプ。 トリガーされたライブダンプのソースについては、パラメーター1の値を参照してください。

(このコードは実際のバグチェックには使用できません。ライブダンプを識別するために使用されます)。

## <a name="see-also"></a>参照

[バグチェックコードリファレンス](bug-check-code-reference2.md)

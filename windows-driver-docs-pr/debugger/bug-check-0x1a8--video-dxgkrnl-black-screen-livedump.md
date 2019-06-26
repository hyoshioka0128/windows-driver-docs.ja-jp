---
title: バグ チェック 0x1A8 VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP
description: VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP のバグ チェックでは、0x000001A8 の値を持ちます。 黒い画面シナリオのユーザーが開始した DXGKRNL ライブ ダンプが発生したことを示します。
keywords:
- バグ チェック 0x1A8 VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP
- VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP
ms.date: 01/28/2018
topic_type:
- apiref
api_name:
- VIDEO_DXGKRNL_BLACK_SCREEN_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3cea02d7da7313ec0a15204a5cacb95acdc5c989
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362026"
---
# <a name="bug-check-0x1a8-videodxgkrnlblackscreenlivedump"></a>バグ チェック 0x1A8:ビデオ\_DXGKRNL\_黒い\_画面\_LIVEDUMP

ビデオ\_DXGKRNL\_黒い\_画面\_LIVEDUMP バグ チェックが 0x000001A8 の値を持ちます。 黒い画面シナリオのユーザーが開始した DXGKRNL ライブ ダンプが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="videodxgkrnlblackscreenlivedump-parameters"></a>ビデオ\_DXGKRNL\_黒い\_画面\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| DXGKRNL 黒い画面のライブ ダンプ - 以下に示すをトリガーしたソース。|
|2| 予約済み。 |
|3| 予約済み。 |
|4| 予約済み。 |

**ソースの値**


0x1:黒い画面ホットキー DXGKRNL 黒い画面のライブ ダンプの生成

0x2:ボリュームの複合キー DXGKRNL 黒い画面のライブ ダンプの生成

0x4:内部生成された DXGKRNL 黒い画面ライブ ダンプ

0x8:長い電源ボタンを保持 (LPBH) DXGKRNL 黒い画面のライブ ダンプの生成

## <a name="cause"></a>原因
-----

ユーザーは、黒い画面シナリオ DXGKRNL ライブ ダンプを開始します。 トリガーされたライブ ダンプのソースのパラメーター 1 の値を参照してください。 

(このコードは、実際のバグチェックには使用されません。 ライブ ダンプの識別に使用されます)。

## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

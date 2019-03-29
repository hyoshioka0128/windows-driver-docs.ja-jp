---
title: バグ チェック 0x1B0 VIDEO_MINIPORT_FAILED_LIVEDUMP
description: VIDEO_MINIPORT_FAILED_LIVEDUMP のバグ チェックでは、0x000001B0 の値を持ちます。 DXGKRNL はビデオのミニポート ドライバーに関する問題を検出し、デバッグ情報を収集するライブのダンプをキャプチャしたことを示します。
keywords:
- バグ チェック 0x1B0 VIDEO_MINIPORT_FAILED_LIVEDUMP
- VIDEO_MINIPORT_FAILED_LIVEDUMP
ms.date: 01/08/2018
topic_type:
- apiref
api_name:
- VIDEO_MINIPORT_FAILED_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0966bef520c1b939799a1e842a6f393da364ea8
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743569"
---
# <a name="bug-check-0x1b0-videominiportfailedlivedump"></a>バグ チェック 0x1B0 の。ビデオ\_ミニポート\_FAILED\_LIVEDUMP

ビデオ\_ミニポート\_FAILED\_LIVEDUMP バグ チェックが 0x000001B0 の値を持ちます。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="videominiportfailedlivedump-parameters"></a>ビデオ\_ミニポート\_FAILED\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| 理由コード。 値:0x1:*デバイスを追加します。* 0x2:*デバイスの起動に失敗しました。*|
|2| NTSTATUS|
|3| 予約済み。 |
|4| 予約済み。 |


## <a name="cause"></a>原因
-----
DXGKRNL では、問題を検出しましたしがデバッグ情報を収集するライブのダンプをキャプチャします。 これらの livedumps は、ビデオのミニポート ドライバーが失敗したときに、dxgkrnl によってトリガーされます。

(このコードは、実際のバグチェックには使用されません。 ライブ ダンプの識別に使用されます)。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

 


 





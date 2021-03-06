---
title: バグ チェック 0x142 VIDEO_TDR_APPLICATION_BLOCKED
description: VIDEO_TDR_APPLICATION_BLOCKED のバグ チェックでは、0x00000142 の値を持ちます。 これは、アプリケーションがグラフィックス ハードウェアへのアクセスがブロックされたことを示します。
ms.assetid: B97FCA51-C368-4144-A364-50135A8DE836
keywords:
- バグ チェック 0x142 VIDEO_TDR_APPLICATION_BLOCKED
- VIDEO_TDR_APPLICATION_BLOCKED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_TDR_APPLICATION_BLOCKED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 28d7e0851443eec0d51513d8e8e0b50bbc0439be
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866491"
---
# <a name="bug-check-0x142-videotdrapplicationblocked"></a>バグ チェック 0x142:ビデオ\_TDR\_アプリケーション\_ブロック


ビデオ\_TDR\_アプリケーション\_ブロック済みのバグ チェックが 0x00000142 の値を持ちます。 これは、アプリケーションがグラフィックス ハードウェアへのアクセスがブロックされたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="videotdrapplicationblocked-parameters"></a>ビデオ\_TDR\_アプリケーション\_ブロックされているパラメーター


| パラメーター | 説明                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 内部の TDR 復旧コンテキストへの省略可能なポインター (TDR\_RECOVERY\_コンテキスト)。 |
| 2         | 担当のデバイス ドライバー モジュール (例: 所有者タグ) へのポインター。          |
| 3         | 2 番目のドライバーの特定バケット キー。                                |
| 4         | GPU へのアクセスがブロックされるプロセスの id。                     |

 

<a name="remarks"></a>コメント
-------

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。
タグ {0} 270A33FD-3DA6-460D-BA89-3C1BAE21E39B} のセカンダリ データには、追加の TDR が含まれているデータに関連します。 使用[ **.enumtag (セカンダリ コールバック データを列挙する)** ](-enumtag--enumerate-secondary-callback-data-.md)データを表示します。

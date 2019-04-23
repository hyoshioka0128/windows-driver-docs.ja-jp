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
ms.openlocfilehash: d4b1bdb01f38eed7bba8993c37717050757a59d7
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902286"
---
# <a name="bug-check-0x142-videotdrapplicationblocked"></a>バグ チェック 0x142:ビデオ\_TDR\_アプリケーション\_ブロック


ビデオ\_TDR\_アプリケーション\_ブロック済みのバグ チェックが 0x00000142 の値を持ちます。 これは、アプリケーションがグラフィックス ハードウェアへのアクセスがブロックされたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="videotdrapplicationblocked-parameters"></a>ビデオ\_TDR\_アプリケーション\_ブロックされているパラメーター


| パラメーター | 説明                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 内部の TDR 復旧コンテキストへの省略可能なポインター (TDR\_RECOVERY\_コンテキスト)。 |
| 2         | 担当のデバイス ドライバー モジュール (例: 所有者タグ) へのポインター。          |
| 3         | 2 番目のドライバーの特定バケット キー。                                |
| 4         | GPU へのアクセスがブロックされるプロセスの id。                     |

 

<a name="remarks"></a>注釈
-------

[ **! 分析**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。
タグ {0} 270A33FD-3DA6-460D-BA89-3C1BAE21E39B} のセカンダリ データには、追加の TDR が含まれているデータに関連します。 使用[ **.enumtag (セカンダリ コールバック データを列挙する)** ](-enumtag--enumerate-secondary-callback-data-.md)データを表示します。

 

 





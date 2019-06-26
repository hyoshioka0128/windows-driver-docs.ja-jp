---
title: バグ チェック 0x141 VIDEO_ENGINE_TIMEOUT_DETECTED
description: VIDEO_ENGINE_TIMEOUT_DETECTED のバグ チェックでは、0x00000141 の値を持ちます。 これは、エンジンは、適切なタイミングで応答に失敗したディスプレイの 1 つを示します。
ms.assetid: 0912495D-DE6D-4064-BD66-DA6145889821
keywords:
- バグ チェック 0x141 VIDEO_ENGINE_TIMEOUT_DETECTED
- VIDEO_ENGINE_TIMEOUT_DETECTED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_ENGINE_TIMEOUT_DETECTED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff521b394cba97ec24344394ee14ad2a62ff3a7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367808"
---
# <a name="bug-check-0x141-videoenginetimeoutdetected"></a>バグ チェック 0x141:VIDEO\_ENGINE\_TIMEOUT\_DETECTED


ビデオ\_エンジン\_タイムアウト\_検出されたバグ チェックが 0x00000141 の値を持ちます。 これは、エンジンは、適切なタイミングで応答に失敗したディスプレイの 1 つを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="videoenginetimeoutdetected-parameters"></a>VIDEO\_ENGINE\_TIMEOUT\_DETECTED Parameters


| パラメーター | 説明                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 内部の TDR 復旧コンテキストへの省略可能なポインター (TDR\_RECOVERY\_コンテキスト)。 |
| 2         | 担当のデバイス ドライバー モジュール (例: 所有者タグ) へのポインター。          |
| 3         | 2 番目のドライバーの特定バケット キー。                                |
| 4         | 省略可能な内部のコンテキスト依存するデータ。                                   |

 

<a name="remarks"></a>注釈
-------

タグ {0} 270A33FD-3DA6-460D-BA89-3C1BAE21E39B} のセカンダリ データには、追加の TDR が含まれているデータに関連します。 .Enumtag を使用すると、データを表示します。

 

 





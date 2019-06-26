---
title: バグ チェック 0x13C INVALID_IO_BOOST_STATE
description: INVALID_IO_BOOST_STATE のバグ チェックでは、0x0000013C の値を持ちます。 これは、無効な I/O boost 状態、スレッドが終了していることを示します。 スレッドの終了時にゼロがあります。
ms.assetid: BDCD8A3A-1F26-41A4-95B0-9B2CEBD333AC
keywords:
- バグ チェック 0x13C INVALID_IO_BOOST_STATE
- INVALID_IO_BOOST_STATE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_IO_BOOST_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2919734345d150adf43193062a182d29fa575fec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367828"
---
# <a name="bug-check-0x13c-invalidiobooststate"></a>バグ チェック 0x13C:無効な\_IO\_BOOST\_状態


無効な\_IO\_BOOST\_状態のバグ チェックが 0x0000013C の値を持ちます。 これは、無効な I/O boost 状態、スレッドが終了していることを示します。 スレッドの終了時にゼロがあります。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="invalidiobooststate-parameters"></a>無効な\_IO\_BOOST\_状態パラメーター


| パラメーター | 説明                                             |
|-----------|---------------------------------------------------------|
| 1         | スレッドをブーストの無効な状態へのポインター |
| 2         | Boost 状態やスロットルの現在の数                   |
| 3         | 予約済み                                                |
| 4         | 予約済み                                                |

 

 

 





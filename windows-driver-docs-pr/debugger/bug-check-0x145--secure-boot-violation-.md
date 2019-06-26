---
title: バグ チェック 0x145 SECURE_BOOT_VIOLATION
description: SECURE_BOOT_VIOLATION のバグ チェックでは、0x00000145 の値を持ちます。 これは、セキュリティで保護された Boot ポリシーの適用が起動しないことを示します。
ms.assetid: C877C655-D94D-45B5-82DB-1361F0B020D2
keywords:
- バグ チェック 0x145 SECURE_BOOT_VIOLATION
- SECURE_BOOT_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SECURE_BOOT_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6d9c950d1cc4409da6b6be516ddfc0800b7398e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367800"
---
# <a name="bug-check-0x145-securebootviolation"></a>バグ チェック 0x145:セキュリティで保護された\_ブート\_違反


SECURE\_ブート\_違反のバグ チェックが 0x00000145 の値を持ちます。 これは、セキュリティで保護された Boot ポリシーの適用が無効なポリシーまたは必要な操作が完了しなくなるため開始できませんでしたを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="securebootviolation-parameters"></a>セキュリティで保護された\_ブート\_違反パラメーター


| パラメーター | 説明                        |
|-----------|------------------------------------|
| 1         | エラーのステータス コード。    |
| 2         | セキュア ブートのポリシーのアドレス。 |
| 3         | セキュア ブートのポリシーのサイズ。    |
| 4         | 予約済み                           |

 

 

 





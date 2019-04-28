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
ms.openlocfilehash: 9ed08b998b3cb8652abad4610dc8f783135d5299
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360446"
---
# <a name="bug-check-0x145-securebootviolation"></a>バグ チェック 0x145:セキュリティで保護された\_ブート\_違反


SECURE\_ブート\_違反のバグ チェックが 0x00000145 の値を持ちます。 これは、セキュリティで保護された Boot ポリシーの適用が無効なポリシーまたは必要な操作が完了しなくなるため開始できませんでしたを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="securebootviolation-parameters"></a>セキュリティで保護された\_ブート\_違反パラメーター


| パラメーター | 説明                        |
|-----------|------------------------------------|
| 1         | エラーのステータス コード。    |
| 2         | セキュア ブートのポリシーのアドレス。 |
| 3         | セキュア ブートのポリシーのサイズ。    |
| 4         | 予約済み                           |

 

 

 





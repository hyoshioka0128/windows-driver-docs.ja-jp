---
title: バグチェック 0xE NO_USER_MODE_CONTEXT
description: NO_USER_MODE_CONTEXT のバグチェックには0x0000000E の値が含まれています。このバグチェックは非常にまれです。
ms.assetid: 0c3b3da9-c9e6-443d-9087-9bee9aa1e41a
keywords:
- バグチェック 0xE NO_USER_MODE_CONTEXT
- NO_USER_MODE_CONTEXT
ms.date: 06/21/2019
topic_type:
- apiref
api_name:
- NO_USER_MODE_CONTEXT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 02a3f23810eafc9b2b0e1cbcc556bd292cba0d9a
ms.sourcegitcommit: 5f22002ceaf9dccd0d761327a1bb1edce4fe94f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567185"
---
# <a name="bug-check-0xe-no_user_mode_context"></a>バグチェック 0xE: NO\_USER\_MODE\_CONTEXT

NO\_USER\_MODE\_コンテキストのバグチェックには、0x0000000E の値が含まれています。

システムスレッドを開始するプロセスでは、最初のスレッドプロシージャから制御が戻ると、バグチェックが実行されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

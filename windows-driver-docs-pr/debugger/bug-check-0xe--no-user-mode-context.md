---
title: バグチェック 0xE NO_USER_MODE_CONTEXT
description: NO_USER_MODE_CONTEXT のバグチェックの値が0x0000000E になっています。このバグチェックは非常に頻繁に行われます。
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
ms.openlocfilehash: da67bd6925996195cf3ec74ed7a94cf1f3523ce2
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534525"
---
# <a name="bug-check-0xe-no_user_mode_context"></a>バグチェック 0xE: \_ ユーザー \_ モード \_ コンテキストがありません

NO \_ USER \_ MODE \_ コンテキストのバグチェックには、0x0000000E の値があります。

システムスレッドを開始するプロセスでは、最初のスレッドプロシージャから制御が戻ると、バグチェックが実行されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

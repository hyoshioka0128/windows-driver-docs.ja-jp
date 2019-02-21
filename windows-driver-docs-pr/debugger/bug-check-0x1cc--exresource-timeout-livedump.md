---
title: バグ チェック 1CC EXRESOURCE_TIMEOUT_LIVEDUMP
description: EXRESOURCE_TIMEOUT_LIVEDUMP のバグ チェックでは、0x000001CC の値を持ちます。
keywords:
- バグ チェック 0x1CC EXRESOURCE_TIMEOUT_LIVEDUMP
- EXRESOURCE_TIMEOUT_LIVEDUMP
ms.date: 04/19/2018
topic_type:
- apiref
api_name:
- EXRESOURCE_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f38d5678d95a936a605ba1269d30d479c8ca3bd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552176"
---
# <a name="bug-check-bug-check-0x1cc-exresourcetimeoutlivedump"></a>チェックのバグ チェック 0x1CC をバグします。EXRESOURCE\_タイムアウト\_LIVEDUMP

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

EXRESOURCE_TIMEOUT_LIVEDUMP のバグ チェックでは、0x000001CC の値を持ちます。

カーネルに次がタイムアウトしました。これは、デッドロック状態またはパフォーマンスの問題の可能性があるため、激しい競合に示していることができます。


## <a name="exresourcetimeoutlivedump-parameters"></a>EXRESOURCE\_タイムアウト\_LIVEDUMP パラメーター

次のパラメーターは、ブルー スクリーンに表示されます。

パラメーター | 説明 
|---------|--------------|
1 | タイムアウトするスケジュールを作成します。
2 | スレッドのタイムアウトを検出
3 | 次の競合の数
4 | 構成されたタイムアウト (秒)




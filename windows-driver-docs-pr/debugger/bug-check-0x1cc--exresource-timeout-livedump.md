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
ms.openlocfilehash: 1231e2732924fa118b67ec0c90d25cc8ae941926
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238971"
---
# <a name="bug-check-bug-check-0x1cc-exresourcetimeoutlivedump"></a>チェックのバグ チェック 0x1CC をバグします。EXRESOURCE\_タイムアウト\_LIVEDUMP

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


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


## <a name="see-also"></a>関連項目
----------

[バグ チェック コード リファレンス](bug-check-code-reference2.md)


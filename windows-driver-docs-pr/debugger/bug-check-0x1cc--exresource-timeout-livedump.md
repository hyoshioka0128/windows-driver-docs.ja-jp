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
ms.openlocfilehash: 131d6bfc1076e03d7e940384229218019ca70998
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519692"
---
# <a name="bug-check-bug-check-0x1cc-exresourcetimeoutlivedump"></a>チェックのバグ チェック 0x1CC をバグします。EXRESOURCE\_タイムアウト\_LIVEDUMP

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


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

[バグチェック コード リファレンス](bug-check-code-reference2.md)


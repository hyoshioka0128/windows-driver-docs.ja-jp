---
title: バグチェック 1CC EXRESOURCE_TIMEOUT_LIVEDUMP
description: EXRESOURCE_TIMEOUT_LIVEDUMP バグチェックの値は0x000001CC です。
keywords:
- バグチェック 0x1CC EXRESOURCE_TIMEOUT_LIVEDUMP
- EXRESOURCE_TIMEOUT_LIVEDUMP
ms.date: 04/19/2018
topic_type:
- apiref
api_name:
- EXRESOURCE_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b65027cbaa9c47cc30079bb66d6e2fff4eb999da
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851285"
---
# <a name="bug-check-0x1cc-exresource_timeout_livedump"></a>バグチェック 0x1CC: EXRESOURCE \_ TIMEOUT \_ LIVEDUMP

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


EXRESOURCE_TIMEOUT_LIVEDUMP バグチェックの値は0x000001CC です。

カーネルの資源がタイムアウトしました。これは、パフォーマンスの問題を引き起こす可能性があるデッドロック状態または過剰な競合を示している可能性があります。


## <a name="exresource_timeout_livedump-parameters"></a>EXRESOURCE \_ TIMEOUT \_ LIVEDUMP パラメーター

次のパラメーターがブルースクリーンに表示されます。

パラメーター | 説明 
|---------|--------------|
1 | タイムアウトした場合は、
2 | タイムアウトを検出したスレッド
3 | ÷資源の競合数
4 | 構成されたタイムアウト (秒)


## <a name="see-also"></a>参照
----------

[バグ チェック コード リファレンス](bug-check-code-reference2.md)


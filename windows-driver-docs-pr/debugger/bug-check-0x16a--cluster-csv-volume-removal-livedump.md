---
title: バグ チェック 0x16A CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP
description: CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP のバグ チェックでは、0x0000016A の値を持ちます。 これは、クラスター共有ボリューム マネージャー ボリュームの削除要求がタイムアウトしたことを示します。
keywords:
- バグ チェック 0x16A CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP
- CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: db92f67ae3f30758405554c82c1b97890686f5ec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367737"
---
# <a name="bug-check-0x16a-clustercsvvolumeremovallivedump"></a>バグ チェック 0x16A:クラスター\_CSV\_ボリューム\_削除\_LIVEDUMP

クラスター\_CSV\_ボリューム\_削除\_LIVEDUMP バグ チェックが 0x0000016A の値を持ちます。 これは、クラスター共有ボリューム マネージャー ボリュームの削除要求がタイムアウトしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。



## <a name="clustercsvvolumeremovallivedump-parameters"></a>クラスター\_CSV\_ボリューム\_削除\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| クラスターのサービスの PID|
|2| 予約済み。|
|3| 予約済み。|
|4| 予約済み。|

## <a name="cause"></a>原因
-----
クラスター共有ボリューム マネージャー ボリュームの削除要求がタイムアウトしました。

システムでは、遅延の分析のためのライブのダンプを生成します。

(このコード決してできますの実際のバグチェック。)

## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[バグチェック コード リファレンス](bug-check-code-reference2.md)





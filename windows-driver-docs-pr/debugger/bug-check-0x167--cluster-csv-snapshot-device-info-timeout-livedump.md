---
title: バグ チェック 0x167 CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP
description: CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP のバグ チェックでは、0x00000167 の値を持ちます。 これは、スナップショット情報を照会する volsnap、クラスター サービスの呼び出し時間がかかりすぎたことを示します。
keywords:
- バグ チェック 0x167 CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP
- CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69bff42db35873b9a84a6bfac6d9b37aa7dfce62
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519961"
---
# <a name="bug-check-0x167-clustercsvsnapshotdeviceinfotimeoutlivedump"></a>バグ チェック 0x167:クラスター\_CSV\_スナップショット\_デバイス\_情報\_タイムアウト\_LIVEDUMP

クラスター\_CSV\_スナップショット\_デバイス\_情報\_タイムアウト\_LIVEDUMPP バグ チェックが 0x00000167 の値を持ちます。 これは、スナップショット情報を照会する volsnap、クラスター サービスの呼び出し時間がかかりすぎたことを示します。


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。



## <a name="clustercsvsnapshotdeviceinfotimeoutlivedump-parameters"></a>クラスター\_CSV\_スナップショット\_デバイス\_情報\_タイムアウト\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| サービスの PID をクラスターします。|
|2| Volsnap クエリを処理するスレッドの TID します。|
|3| このパラメーターが 1 の場合の値を持つ CSV ボリュームの中にタイムアウトがアクティブな場合は 2 分 CSV ボリュームの停止後にタイムアウトします。|
|4| 予約済み。|


## <a name="cause"></a>原因
-----

スナップショット情報を照会する volsnap、クラスター サービスの呼び出し時間がかかりすぎました。

(このコード決してできますの実際のバグチェック。)

## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[バグチェック コード リファレンス](bug-check-code-reference2.md)





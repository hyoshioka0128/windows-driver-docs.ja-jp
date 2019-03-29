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
ms.openlocfilehash: 2f3cbf5fb372618d8ac050345ce365ea33786c85
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743537"
---
# <a name="bug-check-0x167-clustercsvsnapshotdeviceinfotimeoutlivedump"></a>バグ チェック 0x167 の。クラスター\_CSV\_スナップショット\_デバイス\_情報\_タイムアウト\_LIVEDUMP

クラスター\_CSV\_スナップショット\_デバイス\_情報\_タイムアウト\_LIVEDUMPP バグ チェックが 0x00000167 の値を持ちます。 これは、スナップショット情報を照会する volsnap、クラスター サービスの呼び出し時間がかかりすぎたことを示します。


**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


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

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[バグチェック コード リファレンス](bug-check-code-reference2.md)





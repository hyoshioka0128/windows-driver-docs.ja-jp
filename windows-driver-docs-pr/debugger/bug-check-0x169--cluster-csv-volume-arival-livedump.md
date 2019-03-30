---
title: バグ チェック 0x169 CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP
description: CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP のバグ チェックでは、0x00000169 の値を持ちます。 これは、クラスター共有ボリューム マネージャーは、新しいボリューム デバイス オブジェクトを作成するよう依頼され、ボリュームが時間に到着していないことを示します。
keywords:
- バグ チェック 0x169 CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP
- CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b764f08edc97637767c3480c76247d06be68440a
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743558"
---
# <a name="bug-check-0x169-clustercsvvolumearrivallivedump"></a>バグ チェック 0x169 の。クラスター\_CSV\_ボリューム\_到着\_LIVEDUMP

クラスター\_CSV\_ボリューム\_到着\_LIVEDUMP バグ チェックが 0x00000169 の値を持ちます。 これは、クラスター共有ボリューム マネージャーは、新しいボリューム デバイス オブジェクトを作成するよう依頼され、ボリュームが時間に到着していないことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="clustercsvvolumearrivallivedump-parameters"></a>クラスター\_CSV\_ボリューム\_到着\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| サービスの PID をクラスターします。 |
|2| 予約済み。|
|3| 予約済み。|
|4| 予約済み。|


## <a name="cause"></a>原因
-----

クラスター共有ボリューム マネージャーは、新しいボリューム デバイス オブジェクトを作成するよう依頼され、ボリュームが時間に到着していません。

システムでは、遅延の分析のためのライブのダンプを生成します。

(このコード決してできますの実際のバグチェック。)

## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[バグチェック コード リファレンス](bug-check-code-reference2.md)




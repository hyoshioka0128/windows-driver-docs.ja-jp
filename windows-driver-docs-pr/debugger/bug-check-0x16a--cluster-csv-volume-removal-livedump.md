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
ms.openlocfilehash: f39f8917244fc2ed35e1f60a6cb9d022689e5d60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352599"
---
# <a name="bug-check-0x16a-clustercsvvolumeremovallivedump"></a>バグ チェック 0x16A:クラスター\_CSV\_ボリューム\_削除\_LIVEDUMP

クラスター\_CSV\_ボリューム\_削除\_LIVEDUMP バグ チェックが 0x0000016A の値を持ちます。 これは、クラスター共有ボリューム マネージャー ボリュームの削除要求がタイムアウトしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。



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

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[バグチェック コード リファレンス](bug-check-code-reference2.md)





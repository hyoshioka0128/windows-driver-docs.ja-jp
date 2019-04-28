---
title: パケット データ サービスの損失と復旧
description: パケット データ サービスの損失と復旧
ms.assetid: 1e9d6c34-f7fc-47e9-aa52-409b9e9ff4f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 193810084e1648ec7274f8b4b88a1e45f2af2df4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365951"
---
# <a name="losing-and-regaining-packet-data-service"></a>パケット データ サービスの損失と復旧


次の図は、ミニポート ドライバーは、さまざまな間隔の信号強度とパケットのサービスを失うときに従う必要プロセスを示します。 太字のラベルは、OID 識別子またはトランザクションのフロー制御を通常のテキストに表示されるラベル OID 構造内で重要なフラグ。

![失われると、パケット データ サービス用の信号を取り戻しますを示す図](images/wwanregainingpacketdataservice.png)

を失われた後のパケット データ サービスを回復するには、次の手順を使用します。

1.  ミニポート ドライバー送信 NDIS\_WWAN\_リンク\_MB サービスの状態。

2.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931) MB サービスにします。

3.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931) MB サービスにします。

4.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931) MB サービスにします。

5.  ミニポート ドライバー送信 NDIS\_WWAN\_登録\_MB サービスの状態。

6.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567850) MB サービスにします。

7.  ミニポート ドライバー送信[ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391) MB サービスにします。

8.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567931) MB サービスにします。

 

 






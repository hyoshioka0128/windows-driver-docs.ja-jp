---
title: パケット データ サービスの損失と復旧
description: パケット データ サービスの損失と復旧
ms.assetid: 1e9d6c34-f7fc-47e9-aa52-409b9e9ff4f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e3b35a3c1f2e36830098e53ab0773dc062a333
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356213"
---
# <a name="losing-and-regaining-packet-data-service"></a>パケット データ サービスの損失と復旧


次の図は、ミニポート ドライバーは、さまざまな間隔の信号強度とパケットのサービスを失うときに従う必要プロセスを示します。 太字のラベルは、OID 識別子またはトランザクションのフロー制御を通常のテキストに表示されるラベル OID 構造内で重要なフラグ。

![失われると、パケット データ サービス用の信号を取り戻しますを示す図](images/wwanregainingpacketdataservice.png)

を失われた後のパケット データ サービスを回復するには、次の手順を使用します。

1.  ミニポート ドライバー送信 NDIS\_WWAN\_リンク\_MB サービスの状態。

2.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) MB サービスにします。

3.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) MB サービスにします。

4.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) MB サービスにします。

5.  ミニポート ドライバー送信 NDIS\_WWAN\_登録\_MB サービスの状態。

6.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service) MB サービスにします。

7.  ミニポート ドライバー送信[ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state) MB サービスにします。

8.  ミニポート ドライバー送信[ **NDIS\_WWAN\_信号\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) MB サービスにします。

 

 






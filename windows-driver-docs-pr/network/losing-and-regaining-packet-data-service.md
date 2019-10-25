---
title: パケット データ サービスの損失と復旧
description: パケット データ サービスの損失と復旧
ms.assetid: 1e9d6c34-f7fc-47e9-aa52-409b9e9ff4f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91c883bed182a18c5150e34c363038c87ed62e47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844139"
---
# <a name="losing-and-regaining-packet-data-service"></a>パケット データ サービスの損失と復旧


次の図は、さまざまな間隔でシグナルの強さとパケットサービスが失われた場合に、ミニポートドライバーが従う必要があるプロセスを示しています。 太字のラベルは OID 識別子またはトランザクションフロー制御で、通常のテキストのラベルは OID 構造内の重要なフラグです。

![パケットデータサービスの紛失および取り戻し信号を示す図](images/wwanregainingpacketdataservice.png)

パケットデータサービスが失われた後に回復するには、次の手順を実行します。

1.  ミニポートドライバーは、NDIS\_WWAN\_LINK\_状態を MB サービスに送信します。

2.  ミニポートドライバーは、 [**NDIS\_WWAN\_SIGNAL\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)を MB サービスに送信します。

3.  ミニポートドライバーは、 [**NDIS\_WWAN\_SIGNAL\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)を MB サービスに送信します。

4.  ミニポートドライバーは、 [**NDIS\_WWAN\_SIGNAL\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)を MB サービスに送信します。

5.  ミニポートドライバーは、NDIS\_WWAN\_\_の状態を MB サービスに登録します。

6.  ミニポートドライバーは、 [**NDIS\_ステータス\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)を MB サービスに送信します。

7.  ミニポートドライバーは、 [**NDIS\_STATUS\_LINK\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)を MB サービスに送信します。

8.  ミニポートドライバーは、 [**NDIS\_WWAN\_SIGNAL\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)を MB サービスに送信します。

 

 






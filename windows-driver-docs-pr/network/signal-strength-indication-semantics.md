---
title: 信号強度表示セマンティクス
description: 信号強度表示セマンティクス
ms.assetid: d28476f8-d567-4fe0-9cb9-4a78d8b0e05b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0031acac5897c77cb4ba0072fcdc7875d0ea04aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841919"
---
# <a name="signal-strength-indication-semantics"></a>信号強度表示セマンティクス


次の図は、信号強度の表示を処理するためにミニポートドライバーが従う必要があるプロセスを示しています。 MB サービスは、現在のデバイスのシグナルの強さと、デバイスがアイドル状態になっている時間に基づいて、シグナルの強さとレポートのしきい値と間隔を調整します。 これらのアクションは、通常、MB サービスによって提供される電源管理機能の一部として実行されます。 太字のラベルは OID 識別子またはトランザクションフロー制御で、通常のテキストのラベルは OID 構造内の重要なフラグです。

![ミニポートドライバーがシグナルの強さを処理するために従う必要があるプロセスを示す図](images/wwansignalstrength.png)

シグナル強度のインジケーターを更新するには、次の手順に従います。

1.  ミニポートドライバーは、 [**NDIS\_WWAN\_SIGNAL\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)を MB サービスに送信します。

2.  MB サービスは、 [OID\_WWAN\_SIGNAL\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)をミニポートドライバーに送信します。 ミニポートドライバーは、要求を受信したことを示す一時的な受信確認 (NDIS\_の状態\_表示\_) で応答し、要求された情報を後で通知を送信します。

3.  ミニポートドライバーは、NDIS\_ステータス\_WWAN\_成功を MB サービスに送信します。

4.  ミニポートドライバーは、 [**NDIS\_WWAN\_SIGNAL\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)を MB サービスに送信します。

5.  MB サービスは、 [OID\_WWAN\_SIGNAL\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)をミニポートドライバーに送信します。 ミニポートドライバーは、要求を受信したことを示す一時的な受信確認 (NDIS\_の状態\_表示\_) で応答し、要求された情報を後で通知を送信します。

6.  ミニポートドライバーは、NDIS\_ステータス\_WWAN\_成功を MB サービスに送信します。

7.  MB サービスは、 [OID\_WWAN\_SIGNAL\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)をミニポートドライバーに送信します。 ミニポートドライバーは、要求を受信したことを示す一時的な受信確認 (NDIS\_の状態\_表示\_) で応答し、要求された情報を後で通知を送信します。

8.  ミニポートドライバーは、NDIS\_ステータス\_WWAN\_成功を MB サービスに送信します。

9.  ミニポートドライバーは、 [**NDIS\_WWAN\_SIGNAL\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)を MB サービスに送信します。

 

 






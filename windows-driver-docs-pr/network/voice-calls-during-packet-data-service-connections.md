---
title: パケット データ サービス接続時の音声通話
description: パケット データ サービス接続時の音声通話
ms.assetid: 441d2fea-eb39-4af5-a8de-c288c81be99a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976fdb043cc22875c050b64c46ce3ccb72cc2e87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842941"
---
# <a name="voice-calls-during-packet-data-service-connections"></a>パケット データ サービス接続時の音声通話


次の図は、パケットデータサービスがアクティブになっているときに、電話をかけたときにミニポートドライバーが従う必要があるプロセスを示しています。 図では例として1xRTT を使用しますが、この手順は他のエアインターフェイスにも当てはまります。 次の図に記載されているプロセスは、OID\_WWAN\_デバイス\_CAPS*クエリ*に応答して、 **WwanVoiceClass**メンバーで**WwanVoiceClassSeparateVoiceData**を返すミニポートドライバーにのみ適用されます。申請. 太字のラベルは OID 識別子またはトランザクションフロー制御を表し、通常のテキストのラベルは OID 構造内の重要なフラグを表します。

![パケットデータサービスがアクティブになっているときに、電話をかけたときにミニポートドライバーが従う必要があるプロセスを示す図](images/wwanvoicecalls.png)

この手順では、着信音声通話を受け入れると、既存のすべてのパケット接続が事前に割り込まれていることを前提としています。 OID\_WWAN\_デバイス\_CAP*クエリ*要求に応答して、 **WwanVoiceClass**メンバーの**WwanVoiceClassSimultaneousVoiceData**を返すミニポートドライバーの場合、現在のパケット接続をにすることはできません。影響を受ける.

仕様上、MB サービスでは回線音声がサポートされておらず、サービスも禁止されていることに注意してください。 次の図に記載されているプロセスは、デバイスがデータと回線の両方の音声を処理できるが、一度に1つしか処理できない場合にのみ適用されます。 このプロセスでは、既存の既存のデータ接続よりも音声通話が優先されることを前提としています。 この場合、ミニポートドライバーは、音声通話中にデータ接続を中断する必要があります。 その後、ミニポートドライバーは、MB 接続を自動的に再確立することによって、データサービスを再開する必要があります。

パケットデータサービス接続中の音声通話を処理するには、次の手順に従います。

1.  パケットデータサービス接続を成功させるには、ミニポートドライバーで、 [**ndis\_WWAN\_パケット\_サービス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)通知を MB サービスに送信して、現在の microsoft.visualstudio.ordesigner.dataclass.member の後に ndis を指定する必要があり[ **\_状態\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)通知を MB サービスにリンクして、メディアの接続状態を**MediaConnectStateConnected**として示します。

2.  音声通話が行われるか、または応答すると、ミニポートドライバーは、 **MediaConnectStateDisconnected**としてメディア接続状態を示すために、\_状態通知\_を MB サービスにリンクして、 [**NDIS\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)を送信する必要があります。

3.  その後、ミニポートドライバーは、 **WwanVoiceCallStateInProgress**としてのデバイスの*VoiceCall*状態を示す、 [ **\_コンテキスト\_状態通知の NDIS\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)状態を MB サービスに送信する必要があります。

4.  切断時に、ミニポートドライバーは、 **WwanVoiceCallStateHangup**としてのデバイスの*VoiceCall*状態を示す、\_コンテキスト\_状態通知の NDIS\_\_状態を MB サービスに送信する必要があります。

5.  音声通話が完了すると、デバイスはパケット接続を再開します。 ミニポートドライバーは、 **MediaConnectStateConnected**としてメディアの接続状態を示すために、 [ **\_状態通知\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)を MB サービスにリンクして、NDIS\_の状態を送信する必要があります。

6.  ミニポートドライバーは、現在の Microsoft.visualstudio.ordesigner.dataclass.member を示す NDIS\_WWAN\_パケット\_サービス\_状態通知を MB サービスに送信する必要があります。

 

 






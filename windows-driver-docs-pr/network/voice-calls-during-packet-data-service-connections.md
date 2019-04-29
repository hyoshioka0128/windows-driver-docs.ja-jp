---
title: パケット データ サービス接続時の音声通話
description: パケット データ サービス接続時の音声通話
ms.assetid: 441d2fea-eb39-4af5-a8de-c288c81be99a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b60c20acd9c88d3119c6df8e07f742a93598848c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327592"
---
# <a name="voice-calls-during-packet-data-service-connections"></a>パケット データ サービス接続時の音声通話


次の図は、ミニポート ドライバーが音声通話がパケット データ サービスがアクティブな間に配置した場合に従う必要のあるプロセスを表します。 図は、例として、1 xrtt を使用しますが、手順も、他のエア インターフェイスに適用されます。 次の図に記載されているプロセスが返すミニポート ドライバーにのみ適用されます**WwanVoiceClassSeparateVoiceData**で、 **WwanVoiceClass** OID への応答でメンバー\_WWAN\_デバイス\_CAP*クエリ*要求。 太字表す OID の識別子またはトランザクションのフロー制御には、ラベルと通常のテキストに表示されるラベルは、OID 構造内で重要なフラグを表します。

![ミニポート ドライバーが音声通話がパケット データ サービスがアクティブな間に配置した場合に従う必要のあるプロセスを示す図](images/wwanvoicecalls.png)

プロシージャでは、着信音声通話を承諾と、任意の既存のパケットの接続はかけることを前提としています。 返すミニポート ドライバー **WwanVoiceClassSimultaneousVoiceData**で、 **WwanVoiceClass** OID への応答でメンバー\_WWAN\_デバイス\_キャップ*クエリ*要求、現在のパケットの接続は影響がありません。

注意、仕様では、サービスが禁止されることも MB サービスは、回線の音声をサポートしていません。 プロセスには、次が記載されているグラフィックは、デバイスがときに、一度に 1 つだけですが、データと回線の両方の音声に処理できるだけ適用されます。 プロセスでは、優先順位の音声通話は、潜在的な既存のデータ接続経由で、前提としています。 この場合、ミニポート ドライバーでは、音声通話の間のデータ接続を中断する必要があります。 その後、ミニポート ドライバーでは、MB の接続を自動的に再確立することで、データ サービスを再開する必要があります。

パケット データ サービスへの接続中に音声通話を処理するには、次の手順を使用します。

1.  成功したパケット データ サービスの接続のミニポート ドライバーを送信する必要があります、 [ **NDIS\_WWAN\_パケット\_サービス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567910)現在の DataClass を示す MB サービスに通知が続く、 [ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391) MB に通知メディア接続として状態を示すためにサービス**MediaConnectStateConnected**します。

2.  音声通話が配置または回答、ミニポート ドライバーを送信する必要があります、 [ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391) MB サービスへの通知を示すために、メディア接続の状態として**MediaConnectStateDisconnected**します。

3.  ミニポート ドライバーに送信する必要がありますし、 [ **NDIS\_状態\_WWAN\_コンテキスト\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567843) を示すMBサービスへの通知*VoiceCall*としてデバイスの状態**WwanVoiceCallStateInProgress**します。

4.  切断、ミニポート ドライバーが、NDIS を送信する必要があります\_状態\_WWAN\_コンテキスト\_を示す MB サービスに状態の通知、 *VoiceCall* としてデバイスの状態**WwanVoiceCallStateHangup**します。

5.  デバイスでは、音声通話が完了した後、パケットの接続が再開します。 ミニポート ドライバーに送信する必要があります、 [ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391)メディアを示す MB サービスへの通知と状態の接続**MediaConnectStateConnected**します。

6.  ミニポート ドライバーは、NDIS を送信する必要があります\_WWAN\_パケット\_サービス\_現在 DataClass を示す MB サービスに状態の通知。

 

 






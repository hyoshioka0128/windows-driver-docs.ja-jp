---
title: GPRS SIM-ロックされているデバイス (プロビジョニングされたコンテキスト) を初期化しています
description: プロビジョニングのコンテキストでの GPRS の SIM-ロックされているデバイスの初期化
ms.assetid: 0bbd4842-72ad-445b-9f28-b28e8740f263
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de0b1fc92658e66ac990fc892681556f4bb0a50b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385087"
---
# <a name="initialization-of-a-non-sim-locked-gprs-device-with-a-provisioned-context"></a>プロビジョニングのコンテキストでの GPRS の SIM-ロックされているデバイスの初期化

次の図は、GSM ベース MB デバイスの最適なユーザー エクスペリエンスを表します。 既定のエクスペリエンスには、ユーザーの構成は必要ありません。 登録するネットワークを自動的に選択する、デバイスが構成されていると見なされます。 太字表す OID の識別子またはトランザクションのフロー制御には、ラベルと通常のテキストに表示されるラベルは、OID 構造内で重要なフラグを表します。

![gsm ベース mb デバイスの初期化シーケンスを示す図](images/wwangsmdevinitseq.png)

GSM ベースの SIM-ロックされているデバイスを初期化するには、次の手順を実装します。

1.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_準備\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)デバイスの準備完了状態を識別するために、ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

2.  ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_準備ができて\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info) MB に示す MB サービスに通知をサービスします。MB デバイスの状態が**WwanReadyStateInitialized**します。

3.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_登録\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)デバイスの登録状態を識別するために、ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

4.  ミニポート ドライバーに送信、 [ **NDIS\_状態\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)ことを示す MB サービスに通知しますデバイスの登録モードは**WwanRegistraterModeAutomatic**現在の登録状態と**WwanRegisterStateSearching**します。

5.  後で、デバイスがネットワーク プロバイダーに登録されると、ミニポート ドライバーに送信、要請していない NDIS\_状態\_WWAN\_登録\_ことを示す MB サービスに通知を現在の状態デバイスの登録状態が**WwanRegisterStateHome**します。

6.  デバイスがパケットのサービスにアタッチしようとするとします。 ミニポート ドライバーを要請していない送信パケットのサービスの状態が変更されたときに接続されている、 [ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)パケット サービスを示す MB サービスに通知がアタッチされているし、現在のデータ クラスが**WWAN\_データ\_クラス\_GPRS**します。

7.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_ホーム\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)ミニポート ドライバーにホーム プロバイダーの情報を取得するためのクエリ要求。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_REQUIRED)、要求が受信されると、今後の必要な情報の通知が送信されます。

8.  ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_ホーム\_プロバイダー** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)ホーム プロバイダーを示す MB サービスへの通知詳細情報。

9.  MB サービスに送信します (非ブロッキング) 非同期 OID\_WWAN\_プロビジョニング済み\_ミニポート ドライバーにプロビジョニングされているコンテキストの一覧を取得するコンテキストのクエリを要求します。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

10. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_プロビジョニング済み\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)のリストを含む MB サービスへの通知[ **WWAN\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_context)構造体。

11. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect)パケット データ プロトコル (PDP) コンテキストをアクティブ化するミニポート ドライバーに要求を設定します。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

12. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state) PDP コンテキストを示す MB サービスへの通知アクティブ化されます。

13. ミニポート ドライバーの送信、 [ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)メディアが状態を接続することを示す通知が**MediaConnectStateConnected**します。

 

 






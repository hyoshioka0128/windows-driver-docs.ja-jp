---
title: GPRS SIM-ロックされているデバイス (プロビジョニングされたコンテキスト) を初期化しています
description: プロビジョニングのコンテキストでの GPRS の SIM-ロックされているデバイスの初期化
ms.assetid: 0bbd4842-72ad-445b-9f28-b28e8740f263
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d218bcb55ff87903036f287ec1a0e414a64e4e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323395"
---
# <a name="initialization-of-a-non-sim-locked-gprs-device-with-a-provisioned-context"></a>プロビジョニングのコンテキストでの GPRS の SIM-ロックされているデバイスの初期化

次の図は、GSM ベース MB デバイスの最適なユーザー エクスペリエンスを表します。 既定のエクスペリエンスには、ユーザーの構成は必要ありません。 登録するネットワークを自動的に選択する、デバイスが構成されていると見なされます。 太字表す OID の識別子またはトランザクションのフロー制御には、ラベルと通常のテキストに表示されるラベルは、OID 構造内で重要なフラグを表します。

![gsm ベース mb デバイスの初期化シーケンスを示す図](images/wwangsmdevinitseq.png)

GSM ベースの SIM-ロックされているデバイスを初期化するには、次の手順を実装します。

1.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_準備\_情報](https://msdn.microsoft.com/library/windows/hardware/ff569833)デバイスの準備完了状態を識別するために、ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

2.  ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_準備ができて\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567856) MB に示す MB サービスに通知をサービスします。MB デバイスの状態が**WwanReadyStateInitialized**します。

3.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_登録\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569834)デバイスの登録状態を識別するために、ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

4.  ミニポート ドライバーに送信、 [ **NDIS\_状態\_WWAN\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567857)ことを示す MB サービスに通知しますデバイスの登録モードは**WwanRegistraterModeAutomatic**現在の登録状態と**WwanRegisterStateSearching**します。

5.  後で、デバイスがネットワーク プロバイダーに登録されると、ミニポート ドライバーに送信、要請していない NDIS\_状態\_WWAN\_登録\_ことを示す MB サービスに通知を現在の状態デバイスの登録状態が**WwanRegisterStateHome**します。

6.  デバイスがパケットのサービスにアタッチしようとするとします。 ミニポート ドライバーを要請していない送信パケットのサービスの状態が変更されたときに接続されている、 [ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567850)パケット サービスを示す MB サービスに通知がアタッチされているし、現在のデータ クラスが**WWAN\_データ\_クラス\_GPRS**します。

7.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_ホーム\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/ff569826)ミニポート ドライバーにホーム プロバイダーの情報を取得するためのクエリ要求。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_REQUIRED)、要求が受信されると、今後の必要な情報の通知が送信されます。

8.  ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_ホーム\_プロバイダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567848)ホーム プロバイダーを示す MB サービスへの通知詳細情報。

9.  MB サービスに送信します (非ブロッキング) 非同期 OID\_WWAN\_プロビジョニング済み\_ミニポート ドライバーにプロビジョニングされているコンテキストの一覧を取得するコンテキストのクエリを要求します。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

10. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_プロビジョニング済み\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff567854)のリストを含む MB サービスへの通知[ **WWAN\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff571201)構造体。

11. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/ff569823)パケット データ プロトコル (PDP) コンテキストをアクティブ化するミニポート ドライバーに要求を設定します。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

12. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_コンテキスト\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567843) PDP コンテキストを示す MB サービスへの通知アクティブ化されます。

13. ミニポート ドライバーの送信、 [ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391)メディアが状態を接続することを示す通知が**MediaConnectStateConnected**します。

 

 






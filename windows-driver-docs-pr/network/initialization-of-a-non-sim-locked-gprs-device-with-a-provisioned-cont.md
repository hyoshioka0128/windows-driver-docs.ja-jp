---
title: SIM でロックされていない GPRS デバイスの初期化 (プロビジョニングされたコンテキスト)
description: プロビジョニングされたコンテキストを使用した、SIM でロックされていない GPRS デバイスの初期化
ms.assetid: 0bbd4842-72ad-445b-9f28-b28e8740f263
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9778138857212745a4d9e9d57c1fa56eef91cf11
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824613"
---
# <a name="initialization-of-a-non-sim-locked-gprs-device-with-a-provisioned-context"></a>プロビジョニングされたコンテキストを使用した、SIM でロックされていない GPRS デバイスの初期化

次の図は、GSM ベースの MB デバイスで最適なユーザーエクスペリエンスを示しています。 既定のエクスペリエンスでは、ユーザーの構成は必要ありません。 登録するネットワークを自動的に選択するようにデバイスが構成されていることを前提としています。 太字のラベルは OID 識別子またはトランザクションフロー制御を表し、通常のテキストのラベルは OID 構造内の重要なフラグを表します。

![gsm ベースの mb のデバイス初期化シーケンスを示す図](images/wwangsmdevinitseq.png)

SIM でロックされていない GSM ベースのデバイスを初期化するには、次の手順を実装します。

1.  MB サービスは、デバイスの準備完了状態を識別するために、非同期 (非ブロッキング) [OID\_WWAN\_ready\_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)クエリ要求をミニポートドライバーに送信します。 ミニポートドライバーは、要求を受信したことを示す一時的な受信確認 (NDIS\_の状態\_表示\_) で応答し、要求された情報と共に後で通知を送信します。

2.  ミニポートドライバーは、 [ **\_の NDIS ステータス\_WWAN\_READY\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)通知を mb サービスに送信します。これは mb サービスに、mb デバイスの状態が**WwanReadyStateInitialized**であることを示します。

3.  MB サービスは、デバイスの登録状態を識別するために、非同期 (非ブロッキング) [OID\_WWAN\_\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)クエリ要求をミニポートドライバーに送信します。 ミニポートドライバーは、要求を受信したことを示す一時的な受信確認 (NDIS\_の状態\_表示\_) で応答し、要求された情報と共に後で通知を送信します。

4.  ミニポートドライバーは、デバイスの登録モードが**WwanRegistraterModeAutomatic**であり、現在の状態であることを示す\_状態通知を\_登録するための[**NDIS\_ステータス\_WWAN**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)に送信します。登録状態は、 **Wwanregisterstatesearching**です。

5.  その後、デバイスがネットワークプロバイダーに登録されると、ミニポートドライバーは、要請されていない NDIS\_ステータス\_\_WWAN に送信し、\_状態通知を MB サービスに登録します。これは、の現在の登録状態を示します。デバイスは、 **Wwanregisterstatehome**です。

6.  デバイスはパケットサービスの接続を試みます。 パケットサービスの状態が "接続済み" に変更されると、ミニポートドライバーは、パケットサービスが接続されていることを示す[ **\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)の通知を、要求されていない NDIS\_状態を MB サービスに送信します。現在のデータクラスは、 **WWAN\_data\_クラス\_GPRS**です。

7.  MB サービスは、ホームプロバイダー情報を取得するために、非同期 (非ブロッキング) [OID\_WWAN\_home\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)クエリ要求をミニポートドライバーに送信します。 ミニポートドライバーは、要求を受信した一時的な受信確認 (NDIS\_状態\_表示\_必要) で応答し、要求された情報と共に後で通知を送信します。

8.  ミニポートドライバーは、自宅のプロバイダーの詳細を示す、 [ **\_ホーム\_プロバイダーの通知\_、NDIS\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)を MB サービスに送信します。

9.  MB サービスは、プロビジョニングされたコンテキストの一覧を取得するために、\_コンテキストクエリ要求を送信する非同期 (非ブロッキング) OID をミニポートドライバーに送信\_\_します。 ミニポートドライバーは、要求を受信したことを示す一時的な受信確認 (NDIS\_の状態\_表示\_) で応答し、要求された情報と共に後で通知を送信します。

10. ミニポートドライバーは、wwan [ **\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_context)構造の一覧が含まれている、 [ **\_の\_コンテキスト通知\_wwan\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)を MB サービスに送信します。

11. MB サービスは、非同期 (非ブロッキング) [OID\_WWAN\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect) set 要求をミニポートドライバーに送信して、パケットデータプロトコル (PDP) コンテキストをアクティブ化します。 ミニポートドライバーは、要求を受信したことを示す一時的な受信確認 (NDIS\_の状態\_表示\_) で応答し、要求された情報と共に後で通知を送信します。

12. ミニポートドライバーは、PDP コンテキストがアクティブ化されていることを示す、 [ **\_コンテキスト\_状態通知\_の NDIS\_ステータス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)を MB サービスに送信します。

13. ミニポートドライバーは、 [**NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)通知を送信して、メディアの接続状態が**MediaConnectStateConnected**であることを示します。

 

 






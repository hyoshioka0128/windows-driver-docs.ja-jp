---
title: MB パケット コンテキスト管理
description: MB パケット コンテキスト管理
ms.assetid: 52d72def-8aee-4e04-ad42-1a4537cda899
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1daf9fe67923c3f607af4bde1839ec84d97ff75a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374065"
---
# <a name="mb-packet-context-management"></a>MB パケット コンテキスト管理


このトピックでは、ネットワークの特定のセットを設定するための構成パラメーターは、パケットのコンテキストの管理を説明します、*仮想回線*または*フロー*で MB の物理接続上にレイヤー 2。 GSM ベースのデバイスでは、パケット データ プロトコル (PDP) の概念が該当します。 CDMA ベースのデバイスでは、ネットワーク プロファイルが該当します。

ほとんどの場合、パケットのコンテキストの詳細な設定は Ihv や MB デバイスのネットワーク プロバイダーによって事前にプロビジョニングされるまたは無線通信経由のネットワーク (OTA) を使用してプロビジョニングまたは SMS を使用します。 どちらの場合、エンドユーザー通常必要はありません (たとえば、サービス (QoS)、セキュリティ コードをモバイルの IP、およびなどの品質) の設定のほとんどを提供します。 ただし、エンドユーザーは、ネットワーク アクセスの文字列、username、およびパスワードを提供する必要があります。 これらのユーザー構成可能な設定 MB サービスの観点からのパケットのコンテキストのコンテンツを構成することをお勧めします。

MB ドライバー モデルでは、セットアップまたは WWAN のレイヤー 2 接続を破棄する明示的な OID は提供されません。 代わりに、基になるレイヤー 2 接続を設定して、最後のパケットのコンテキストを非アクティブ化で最初のパケットのコンテキストの結果をアクティブ化が効果的に破棄の基になるレイヤー 2 接続。

MB のドライバー モデルでは、次のように、特定の時点でコンテキストのアクティブなパケットの数に関するこれら 2 つの制約の作成します。

1.  各パケットのコンテキストには、1 回だけがアクティブ化することができます。

2.  特定の時点には、コンテキストを 1 つのパケットのみをアクティブにできます。

MB ドライバー モデルに準拠している任意のミニポート ドライバーを設定する必要があります、 **MaxActivatedContexts**のメンバー、 [ **WWAN\_デバイス\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps)構造体を 1 つへの応答時[OID\_WWAN\_デバイス\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)要求のクエリを実行します。 ミニポート ドライバーでは、1 より大きい値を指定するには、この値を設定、場合でも、MB サービスは、最大で 1 つだけのパケットのコンテキストを有効にする特定の時点を確認します。

パケット コンテキストごとに 1 つだけの時間がアクティブにできるため、アクティブ化した後、仮想回線を識別するために静的パケットのコンテキスト識別子を使用できます。 最初の制約をまだ保持している限り、この静的識別子の使用がまだ有効です。

パケットのコンテキストの管理の詳細については、次を参照してください[OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)と[OID\_WWAN\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect).

 

 






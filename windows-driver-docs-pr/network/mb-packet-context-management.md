---
title: MB パケット コンテキスト管理
description: MB パケット コンテキスト管理
ms.assetid: 52d72def-8aee-4e04-ad42-1a4537cda899
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 824442ce9afe74e4b97a4b928518f38cb4f68cdf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844275"
---
# <a name="mb-packet-context-management"></a>MB パケット コンテキスト管理


このトピックでは、レイヤー2で物理 MB 接続の上に*仮想回線*または*フロー*を設定するための特定のネットワーク構成パラメーターセットであるパケットコンテキストの管理について説明します。 GSM ベースのデバイスでは、これはパケットデータプロトコル (PDP) の概念に対応します。 CDMA ベースのデバイスでは、これはネットワークプロファイルに対応します。

ほとんどの場合、パケットコンテキストの詳細設定は、Ihv および/または MB デバイスのネットワークプロバイダーによって事前プロビジョニングされているか、ネットワーク経由で無線 (OTA) または SMS を使用してプロビジョニングされています。 どちらの場合も、エンドユーザーは通常、ほとんどの設定 (サービス品質 (QoS)、セキュリティコード、モバイル IP など) を提供する必要はありません。 ただし、エンドユーザーは、ネットワークアクセス文字列、ユーザー名、およびパスワードの入力が必要になる場合があります。 これは、MB サービスの観点からパケットコンテキストの内容を構成する、ユーザーが構成できる設定です。

MB ドライバーモデルでは、WWAN のレイヤー2接続を設定または破棄するための明示的な OID は提供されません。 代わりに、最初のパケットコンテキストをアクティブ化すると、基になるレイヤー2接続が設定され、最後のパケットコンテキストを非アクティブ化すると、実質的には、基になるレイヤー2接続が破棄されます。

MB ドライバーモデルは、次のように、特定の時点のアクティブなパケットコンテキストの数に関して、これら2つの制約に基づいています。

1.  各パケットコンテキストは、1回だけアクティブにすることができます。

2.  任意の時点で、1つのパケットコンテキストのみをアクティブにできます。

MB ドライバーモデルに準拠しているすべてのミニポートドライバーは、OID\_WWAN\_デバイスに応答するときに、 [**wwan\_デバイス\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)構造体の**Maxactivatedcontexts**メンバーを1に設定することが必須です[\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)クエリ要求。 ミニポートドライバーによってこの値が1より大きい値に設定されている場合でも、MB サービスにより、特定の時点で最大1つのパケットコンテキストのみがアクティブになります。

各パケットコンテキストはアクティブにすることができるため、アクティブ化された後に、静的パケットコンテキスト識別子を使用して仮想回線を識別できます。 この静的識別子の使用は、最初の制約が引き続き保持されている限り有効です。

パケットコンテキスト管理の詳細については、「 [oid\_wwan\_プロビジョニング](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)された\_コンテキストと[oid\_WWAN\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect)」を参照してください。

 

 






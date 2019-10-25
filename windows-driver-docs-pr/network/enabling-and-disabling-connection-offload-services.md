---
title: 接続オフロード サービスの有効化と無効化
description: 接続オフロード サービスの有効化と無効化
ms.assetid: 3d353f87-1cd7-483a-b8eb-d45ec3b8f94e
keywords:
- 接続オフロード WDK TCP/IP トランスポート、サービスの有効化
- 接続オフロード WDK TCP/IP トランスポート、サービスの無効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21e76b8c4ef870379e0e4af186e773d872ea4e66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838125"
---
# <a name="enabling-and-disabling-connection-offload-services"></a>接続オフロード サービスの有効化と無効化





プロトコルドライバーは、オブジェクト識別子 (OID) 要求を使用して接続オフロードサービスを有効にします。

タスクオフロードサービスを有効または無効に**する  、** 接続オフロードサービスの有効化または無効化とは異なります。 ミニポートドライバーは、プロトコルドライバーがカプセル化の種類を指定した後に、利用可能なすべてのタスクオフロードサービスをアクティブにします。

 

TCP/IP トランスポートは、ネットワークインターフェイスカード (NIC) の接続オフロード機能を有効または無効にします。これを行うには、 [oid\_tcp\_接続\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-parameters) oid を設定します。 この設定操作では、TCP/IP トランスポートは ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーの\_オフロード\_パラメーター構造に、NDIS\_tcp\_接続を渡します。 (NDIS\_TCP\_接続\_オフロード\_のパラメーターについては、「 [ndis 6.0 tcp chimney オフロードのドキュメント](full-tcp-offload.md)」を参照してください)。

接続オフロードサービスの構成の詳細については、「 [NDIS 6.0 TCP chimney オフロードのドキュメント](full-tcp-offload.md)」の「オフロードターゲットの初期化」を参照してください。

 

 






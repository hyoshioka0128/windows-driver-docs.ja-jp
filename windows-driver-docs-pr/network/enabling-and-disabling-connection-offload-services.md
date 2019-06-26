---
title: 接続オフロード サービスの有効化と無効化
description: 接続オフロード サービスの有効化と無効化
ms.assetid: 3d353f87-1cd7-483a-b8eb-d45ec3b8f94e
keywords:
- 接続の負荷を軽減 WDK TCP/IP トランスポートは、サービスを有効にします。
- 接続の負荷を軽減 WDK TCP/IP トランスポートは、サービスを無効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c031940bf2ea35467aebf7ec82684bd31fea0faa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378689"
---
# <a name="enabling-and-disabling-connection-offload-services"></a>接続オフロード サービスの有効化と無効化





プロトコル ドライバーには、オブジェクト識別子 (OID) 要求と接続のオフロード サービスが有効にします。

**注**  有効化またはタスクのオフロード サービスを無効にすると、有効にするとは異なるまたはオフロード サービスの接続を無効にするとします。 プロトコル ドライバーをカプセル化の種類を指定した後、ミニポート ドライバーはすべての利用可能なタスク オフロード サービス有効にします。

 

TCP/IP トランスポートを有効またはネットワーク インターフェイス カード (NIC) の接続のオフロード機能を無効に設定して、 [OID\_TCP\_接続\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-parameters)OID。 この設定の操作、TCP/IP トランスポートは、NDIS を渡します\_TCP\_接続\_オフロード\_パラメーター構造体、 **InformationBuffer** のメンバー[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 (NDIS について\_TCP\_接続\_オフロード\_パラメーターを参照して[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))。

オフロード サービス接続の構成の詳細についてでのオフロードのターゲットの初期化を参照してください、 [NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md)します。

 

 






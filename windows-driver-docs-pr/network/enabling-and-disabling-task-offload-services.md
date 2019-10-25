---
title: タスク オフロード サービスの有効化と無効化
description: プロトコルドライバーは、OID_OFFLOAD_ENCAPSULATION OID set 要求を発行することによって、基になるミニポートアダプターのタスクオフロードサービスを有効または無効にすることができます。
ms.assetid: cc803af4-d4ed-4b51-9e0e-77443e0eb023
keywords:
- タスクオフロード WDK TCP/IP トランスポート、サービスの有効化
- タスクオフロード WDK TCP/IP transport、サービスの無効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18f6e9c3a95a49e51f4963f6cfb7748f6e255dc1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834781"
---
# <a name="enabling-and-disabling-task-offload-services"></a>タスク オフロード サービスの有効化と無効化


プロトコルドライバーでは、 [oid\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)oid セット要求を発行することによって、基になるミニポートアダプターのタスクオフロードサービスを有効または無効にすることができます。 この OID 要求では、必要なカプセル化の種類を設定し、使用可能なすべてのタスクオフロードサービスをアクティブ化するようにミニポートドライバーに指示します。




[Oid\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)oid セット要求を発行する前に、プロトコルドライバーは、基になるミニポートアダプターが必要なカプセル化の種類をサポートしていることを確認する必要があります。 これを行うには、次の2つの方法があります。

-   プロトコルドライバーが[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数で受信した、 [**NDIS\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造を確認します。
-   \_現在の\_構成クエリ要求に対して、 [OID\_TCP\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)を実行します。

要求されたカプセル化の種類をサポートするタスクオフロードの種類をミニポートドライバーがサポートしている場合、ミニポートドライバーは、 [OID\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)セット要求に応答して、NDIS\_STATUS\_SUCCESS を返す必要があります。 それ以外の場合、ミニポートドライバーは NDIS\_STATUS\_無効な\_パラメーターを返す必要があります。

 

 






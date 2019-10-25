---
title: TCP/IP オフロード管理者インターフェイスの使用
description: TCP/IP オフロード管理者インターフェイスの使用
ms.assetid: 2418e577-17cd-4db7-adb0-44b705e29d38
keywords:
- TCP/IP オフロード WDK ネットワーク、管理者インターフェイス
- WDK TCP/IP トランスポートのオフロード, 管理者インターフェイス
- タスクオフロード WDK TCP/IP トランスポート、管理者インターフェイス
- 接続オフロード WDK TCP/IP トランスポート、管理者インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cd4df27dadc5085d96df98dd29f69986314a16e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842968"
---
# <a name="using-the-tcpip-offload-administrator-interface"></a>TCP/IP オフロード管理者インターフェイスの使用





NDIS 6.0 以降のバージョンでは、ユーザーモードアプリケーション (またはそれ以降のドライバー) は、TCP/IP オフロード機能を有効または無効にすることができます。 システム管理者は、Microsoft Windows Management Instrumentation (WMI) インターフェイスを使用して設定にアクセスできます。 また、ハードウェアでサポートされている場合に有効にできるレジストリ設定によって無効にされている機能が存在する場合もあります。

[Oid\_TCP\_オフロード\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)オブジェクト識別子 (oid) セット要求に応答して、ミニポートドライバーは、 [**NDIS\_OFFLOAD\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造の設定を使用して、現在のオフロードを設定します。ミニポートアダプターの接続のオフロード構成。

NDIS では、要求された設定は、オフロード標準化されたキーワードでレジストリに保持されます。 NDIS がミニポートアダプターを再起動すると、ミニポートドライバーは、オフロード標準化されたキーワードを読み取り、それらを使用して NIC の既定のオフロード構成を設定します。 ミニポートドライバーが標準以外のキーワードもサポートしている場合は、タスクのオフロード設定を変更するときに、ミニポートドライバーによってレジストリが更新されます。 標準化されたキーワードの詳細については、「[ネットワークデバイスの標準化](standardized-inf-keywords-for-network-devices.md)された INF キーワード」を参照してください。

ミニポートドライバーは、 [**NDIS\_offload\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造の内容を使用して、現在報告されているオフロード構成を更新する必要があります。 ミニポートドライバーは、現在の構成を報告する必要があります。タスクオフロード[**ndis\_ステータス\_タスク\_オフロード\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)または接続オフロード NDIS\_状態\_オフロード\_再開状態を示します。 (NDIS の\_ステータス\_オフロード\_再開の詳細については、「 [ndis 6.0 TCP chimney オフロードのドキュメント](full-tcp-offload.md)」を参照してください)。ステータス表示によって、すべてのプロトコルドライバーが新機能の情報で更新されます。

ユーザーモードアプリケーション (またはそれ以降のドライバー) は、 [oid\_tcp\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)を設定する前に、 [\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)oid または[oid\_tcp を使用することができます。\_接続\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)OID を使用して、ミニポートアダプターのハードウェアがサポートできる機能を決定します。 Oid\_TCP\_オフロード\_パラメーター OID を使用すると、[現在\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)oid または[oid\_tcp\_接続\_オフロード\_\_の機能を有効にする\_ことができ @no__t_現在\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config)OID レポートは、現在有効になっていません。

ハードウェアの機能が変更された場合 (たとえば、MUX 中間ドライバーが異なる基になるミニポートアダプターに切り替えたため)、中間ドライバーは、NDIS\_の状態を使用してハードウェアのオフロード機能の変更を報告する必要があり[ **\_タスク\_オフロード\_ハードウェア\_機能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-hardware-capabilities)または[**NDIS\_ステータス\_TCP\_接続\_\_ハードウェア\_機能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-tcp-connection-offload-hardware-capabilities)の状態を示します。

NDIS およびそれ以降のドライバーでは、 [OID\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)oid を使用して、基になるミニポートアダプターのタスクオフロードカプセル化の設定を設定または照会できます。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**NDIS\_オフロード\_カプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)構造が含まれています。

 

 






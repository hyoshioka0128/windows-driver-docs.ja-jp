---
title: TCP/IP オフロード管理者インターフェイスの使用
description: TCP/IP オフロード管理者インターフェイスの使用
ms.assetid: 2418e577-17cd-4db7-adb0-44b705e29d38
keywords:
- TCP/IP のオフロード WDK のネットワー キング、管理者インターフェイス
- WDK TCP/IP トランスポート、管理者インターフェイスの負荷を軽減します。
- タスクのオフロード WDK TCP/IP トランスポート、管理者インターフェイス
- 接続の負荷を軽減 WDK TCP/IP トランスポート、管理者インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8beb0feeed592dba04aff87441dc5ce56812f7e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384371"
---
# <a name="using-the-tcpip-offload-administrator-interface"></a>TCP/IP オフロード管理者インターフェイスの使用





NDIS 6.0 とそれ以降のバージョンでは、ユーザー モード アプリケーション (または上にあるドライバー) を有効にするしたり TCP/IP オフロード機能を無効にできます。 システム管理者は、Microsoft Windows Management Instrumentation (WMI) インターフェイスを介して設定にアクセスできます。 ハードウェアではサポートされている場合に有効にするレジストリ設定を無効になっている機能もあります。

応答、 [OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)オブジェクト識別子 (OID) 要求の設定、ミニポート ドライバーの設定を使用して、 [ **NDIS\_オフロード\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)ミニポート アダプターの現在オフロードまたは接続オフロードの構成を設定する構造体。

NDIS は、標準化されたオフロード キーワードでレジストリに要求された設定を保持します。 NDIS ミニポート アダプターを再起動すると、ミニポート ドライバーがオフロードが標準化されているキーワードを読み込みし、NIC の既定のオフロードの構成の設定にそれらを使用 ミニポート ドライバーでは、非標準のキーワードもサポートする場合は、タスクのオフロード設定を変更するときに、レジストリを更新するため、ミニポート ドライバーが担当します。 標準化されたキーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

ミニポート ドライバーの内容を使用する必要があります、 [ **NDIS\_オフロード\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)現在報告されたを更新する構造体は、構成をオフロードします。 ミニポート ドライバーが現在の構成とタスク オフロードを報告する必要があります[ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config) NDIS 接続の負荷を軽減または\_状態\_オフロード\_再開状態を示す値。 (NDIS について\_状態\_オフロード\_再開を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))。状態の表示により、新しい機能の情報ですべての上位のプロトコルのドライバーが更新されるようになります。

ユーザー モード アプリケーション (または上にあるドライバー) を設定する前に[OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)使用できる、 [OID\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID または[OID\_TCP\_接続\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-hardware-capabilities)OIDミニポート アダプターのハードウェアでサポートできるどのような機能を確認します。 OID を使用\_TCP\_オフロード\_パラメーター OID 機能を有効にする、 [OID\_TCP\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)OID または[OID\_TCP\_接続\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config) OID レポートは現在有効になっています。

中間のドライバーがでオフロード ハードウェア機能のすべての変更を報告する必要があります (たとえば、MUX 中間ドライバーは、ミニポート アダプターを基になる相違に切り替える) ので、ハードウェア機能が変更する場合、 [ **NDIS\_状態\_タスク\_オフロード\_ハードウェア\_機能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-hardware-capabilities)または[ **NDIS\_状態\_TCP\_接続\_オフロード\_ハードウェア\_機能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-tcp-connection-offload-hardware-capabilities)状態を示す値。

NDIS および上にあるドライバーを使用できます、 [OID\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)設定またはタスクを照会する OID は、基になるミニポート アダプターの設定をカプセル化をオフロードします。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造に含まれる、 [ **NDIS\_オフロード\_カプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)構造体。

 

 






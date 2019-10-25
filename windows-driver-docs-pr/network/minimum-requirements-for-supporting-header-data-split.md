---
title: ヘッダー データの分割をサポートするための最小要件
description: ヘッダー データの分割をサポートするための最小要件
ms.assetid: 32ca214a-5103-4472-bbdb-1338188750d9
keywords:
- ヘッダー-データ分割 WDK、要件
- イーサネットフレーム分割 WDK ネットワーク、要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fad56c53ebccc22e167768cf1aa009fd367cd62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844262"
---
# <a name="minimum-requirements-for-supporting-header-data-split"></a>ヘッダー データの分割をサポートするための最小要件





このトピックでは、ヘッダーデータの分割をサポートするためにプロバイダーが満たす必要のある最小要件について説明します。 イーサネットフレームの分割に適用されるルールの完全な一覧については、「[イーサネットフレームの分割](splitting-ethernet-frames.md)」を参照してください。

次の一覧には、ヘッダーデータの分割がサポートされる最小要件が含まれています。

-   プロバイダーは、[ヘッダーデータの分割が使用されていないケース](cases-where-header-data-split-is-not-used.md)について説明するフレームを分割することはできません。

-   プロバイダーは、仮想 LAN (VLAN) タグを[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) structure OOB data に移動する必要があります。 VLAN の要件の詳細については、「[ヘッダーデータの分割によるインジケーターの受信](receive-indications-with-header-data-split.md)」を参照してください。

-   プロバイダーは、オプションを指定せずに IPv4 フレームの分割をサポートする必要があります。 IPv4 フレームの分割の詳細については、「 [Ipv4 フレームの分割](splitting-ipv4-frames.md)」を参照してください。

-   プロバイダーは、拡張ヘッダーのない IPv6 フレームの分割をサポートする必要があります。 IPv6 フレームの分割の詳細については、「 [Ipv6 フレームの分割](splitting-ipv6-frames.md)」を参照してください。

-   プロバイダーは、tcp オプションを指定せず、タイムスタンプオプションだけを使用して、tcp ペイロードでの TCP フレームの分割をサポートする必要があります。 TCP フレームの分割の詳細については、「 [Tcp ペイロードでのフレームの分割](splitting-frames-at-the-tcp-payload.md)」を参照してください。

-   プロバイダーは udp ペイロードでの UDP フレームの分割をサポートする必要があります。 UDP フレームの分割の詳細については、「 [Udp ペイロードでのフレームの分割](splitting-frames-at-the-udp-payload.md)」を参照してください。

-   プロバイダーは、ヘッダーデータ分割初期化属性をサポートする必要があります。 これらの属性の詳細については、「[ヘッダーデータの分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)」を参照してください。

-   プロバイダーは、ヘッダーデータの分割受信を示す要件をサポートする必要があります。たとえば、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)の**nblflags**メンバーのヘッダーデータの分割フラグ\_リスト構造体、ヘッダーサイズの要件、およびデータを設定します。バックフィル要件。 受信要件の詳細については、「[ヘッダーデータの分割による通知の受信](receive-indications-with-header-data-split.md)」を参照してください。

-   プロバイダーは、 [oid\_GEN\_hd\_split\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters) Oid、 [oid\_gen\_hd\_分割\_現在の\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config) OID、 [**NDIS\_STATUS\_hd をサポートする必要があります。現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)の状態の表示、およびレジストリの設定\_分割\_ます。 ヘッダーデータの分割パラメーターと設定の詳細については、「[ヘッダー-データの分割管理と構成](header-data-split-administration-and-configuration.md)」を参照してください。

プロトコルドライバーとフィルタードライバーのヘッダーデータの分割要件の詳細については、「[サポートヘッダー-プロトコルドライバーでのデータの分割とフィルタードライバー](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)」を参照してください。

 

 






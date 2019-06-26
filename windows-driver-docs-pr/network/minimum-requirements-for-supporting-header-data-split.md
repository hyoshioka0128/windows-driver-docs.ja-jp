---
title: ヘッダー データの分割をサポートするための最小要件
description: ヘッダー データの分割をサポートするための最小要件
ms.assetid: 32ca214a-5103-4472-bbdb-1338188750d9
keywords:
- ヘッダー データの分割 WDK、要件
- WDK は、ネットワークの要件を分割するイーサネット フレーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14c8717c3cb38392c6dded5bf147b8e61c121e4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373980"
---
# <a name="minimum-requirements-for-supporting-header-data-split"></a>ヘッダー データの分割をサポートするための最小要件





このトピックでは、プロバイダーは、ヘッダー データの分割をサポートするために満たす必要のある最小要件をまとめたものです。 分割イーサネット フレームに適用される規則の完全な一覧については、次を参照してください。[イーサネット フレームの分割](splitting-ethernet-frames.md)します。

次の一覧には、ヘッダー データの分割のサポートの最小要件が含まれています。

-   プロバイダーは許可されませんフレームの分割、[の場合、ヘッダー データ分割が使用されていない](cases-where-header-data-split-is-not-used.md)トピックについて説明します。

-   プロバイダーは、仮想 LAN (VLAN) タグを移動する必要があります、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) OOB データ構造体します。 VLAN の要件の詳細については、次を参照してください。[ヘッダー データの分割と受信の兆候](receive-indications-with-header-data-split.md)します。

-   プロバイダーでは、オプションを指定せず、分割の IPv4 フレームをサポートする必要があります。 IPv4 のフレームの分割の詳細については、次を参照してください。 [IPv4 フレームの分割](splitting-ipv4-frames.md)します。

-   プロバイダーは、拡張ヘッダーなしの分割の IPv6 フレームをサポートする必要があります。 IPv6 のフレームの分割の詳細については、次を参照してください。 [IPv6 フレームの分割](splitting-ipv6-frames.md)します。

-   プロバイダーは、TCP ペイロードおよびタイムスタンプ オプションのみを使用して TCP オプションなしでの分割の TCP フレームをサポートする必要があります。 TCP フレームの分割の詳細については、次を参照してください。 [TCP ペイロードで分割フレーム](splitting-frames-at-the-tcp-payload.md)します。

-   プロバイダーでは、UDP ペイロードに分割の UDP フレームをサポートする必要があります。 UDP のフレームの分割の詳細については、次を参照してください。 [UDP ペイロードにフレームを分割](splitting-frames-at-the-udp-payload.md)します。

-   プロバイダーは、初期化属性を分割ヘッダー データをサポートする必要があります。 これらの属性の詳細については、次を参照してください。[ヘッダー データの分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)します。

-   プロバイダーは、ヘッダー データの分割をサポートする必要がありますの要件を示す値を受信すると、フラグを分割ヘッダー データの設定を含む、 **NblFlags**のメンバー、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造、ヘッダーのサイズ要件、およびデータ バックフィル要件。 詳細については、受け取った要件を参照してください[ヘッダー データの分割と受信の兆候](receive-indications-with-header-data-split.md)します。

-   プロバイダーをサポートする必要があります、 [OID\_GEN\_HD\_分割\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters) OID、 [OID\_GEN\_HD\_分割\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config) OID、 [ **NDIS\_状態\_HD\_分割\_現在\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状態を示す値、およびレジストリ設定します。 ヘッダー データの分割パラメーターと設定の詳細については、次を参照してください。[ヘッダー データの分割の管理と構成](header-data-split-administration-and-configuration.md)します。

プロトコルおよびフィルター ドライバーのヘッダー データの分割要件の詳細については、次を参照してください。[プロトコル ドライバーとフィルター ドライバーでヘッダー データの分割をサポートしている](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)します。

 

 






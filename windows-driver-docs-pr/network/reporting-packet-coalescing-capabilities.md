---
title: パケット結合機能のレポート
description: パケット結合機能のレポート
ms.assetid: 6118F648-87FE-4B9E-9535-1602F4FF79D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f47c6a37f46c2a80e4f4b7873d4a1fe18dbbb3c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373250"
---
# <a name="reporting-packet-coalescing-capabilities"></a>パケット結合機能のレポート


ミニポート ドライバーは、NDIS を使用して、ネットワーク アダプターの初期化中に、次の機能を登録します。

-   ネットワーク アダプターでサポートされるパケット結合機能。

-   ネットワーク アダプターで現在有効になっているパケット結合機能。

-   ネットワーク アダプター上で現在有効なフィルター処理機能を受信パケットの結合します。

**注**パケットの結合のミニポート ドライバーのサポートを有効または無効にできる、  **\*PacketCoalescing** INF キーワードの設定。 この設定が表示されます、**詳細**ネットワーク アダプターのプロパティ ページ。 パケット結合 INF ファイルの設定の詳細については、次を参照してください。[パケットの結合の標準化された INF キーワード](standardized-inf-keywords-for-packet-coalescing.md)します。



ミニポート ドライバー、パケットの結合とフィルターを通じて基になるネットワーク アダプターの機能の報告、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。 場合、  **\*PacketCoalescing**キーワード、レジストリ設定は、1 つの値を持つ、パケットの結合が有効になっているし、ミニポート ドライバーを初期化します、 **NDIS\_受信\_フィルター\_機能**次のように構造体。

1.  ミニポート ドライバーを初期化します、**ヘッダー**メンバー。 ドライバーのセット、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。

    ドライバーは、パケットの結合をサポートする場合、設定、**リビジョン**のメンバー**ヘッダー** NDIS に\_受信\_フィルター\_機能\_リビジョン\_2 と**サイズ**NDIS メンバー\_SIZEOF\_受信\_フィルター\_機能\_リビジョン\_2。

2.  ミニポート ドライバーの設定、NDIS\_受信\_フィルター\_パケット\_COALESCING\_サポートされている\_ON\_既定\_のキューフラグ**SupportedQueueProperties**メンバー。

    このフラグが設定されている場合、ネットワーク アダプターがハードウェアでの受信マルチキャスト パケットのフィルター処理をサポートする必要があります。 NDIS が送信することで、ネットワーク アダプターにオフロードするマルチキャスト アドレスに基づく、このフィルタ リング[OID\_802\_3\_マルチキャスト\_一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-multicast-list)OID が要求を設定します。

    **注**プロトコル ドライバーはマルチキャスト アドレスの一覧の内容を送信することによって変更できますも[OID\_802\_3\_追加\_マルチキャスト\_アドレス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)[OID\_802\_3\_削除\_マルチキャスト\_アドレス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-delete-multicast-address)要求。 NDIS にこれらの要求を結合する[OID\_802\_3\_マルチキャスト\_一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-multicast-list)OID が要求を設定します。




**注**アダプターが宛先メディア アクセス制御 (MAC) アドレスと一致しませんこの OID セットの要求で指定されたマルチキャスト アドレスのいずれかの受信マルチキャスト パケットを拒否するために必要です。




3.  ミニポート ドライバーの設定、NDIS\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、 **EnabledFilterTypes**メンバー.

    **注**NDIS が設定する必要がありますも場合は、ドライバーは、このフラグを設定、\_受信\_フィルター\_パケット\_COALESCING\_サポートされている\_ON\_既定\_キュー フラグ、 **SupportedQueueProperties**メンバー。 それ以外の場合、NDIS はへの呼び出しは失敗[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes) NDIS を返すことによって\_状態\_不良\_特性。



4.  ミニポート ドライバーの設定、NDIS 場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ドライバーすべてのサポートは、フィルター条件を受け取る必要があります。 ドライバーでは、このサポートをアドバタイズで、次のフラグを設定して、 **SupportedFilterTests**メンバー。

    -   NDIS\_受信\_フィルター\_テスト\_ヘッダー\_フィールド\_等しい\_サポートされています。

    -   NDIS\_受信\_フィルター\_テスト\_ヘッダー\_フィールド\_マスク\_等しい\_サポートされています。

    -   NDIS\_受信\_フィルター\_テスト\_ヘッダー\_フィールド\_いない\_等しい\_サポートされています。

    **注**ミニポート ドライバーは、NDIS を設定していない場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ドライバーは、を設定する必要があります**SupportedFilterTests**メンバーをゼロにします。



5.  ミニポート ドライバーの設定、NDIS 場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ミニポート ドライバーがさまざまな内のデータのフィルタ リングをサポートする必要がありますメディアのフィールドへのアクセス制御 (MAC)、IP version 4 (IPv4) と IP version 6 (IPv6) のヘッダー。 ドライバーでは、このサポートをアドバタイズで、次のフラグを設定して、 **SupportedHeaders**メンバー。

    -   NDIS\_受信\_フィルター\_MAC\_ヘッダー\_サポートされています。

    -   NDIS\_受信\_フィルター\_ARP\_ヘッダー\_サポートされています。

    -   NDIS\_受信\_フィルター\_IPV4\_ヘッダー\_サポートされています。

    -   NDIS\_受信\_フィルター\_IPV6\_ヘッダー\_サポートされています。

    -   NDIS\_受信\_フィルター\_UDP\_ヘッダー\_サポートされています。

    **注**ミニポート ドライバーは、NDIS を設定していない場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ドライバーは、を設定する必要があります**SupportedHeaders**メンバーをゼロにします。



6.  ミニポート ドライバーの設定、NDIS 場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ミニポート ドライバーは、メディア内にあるデータのフィルター処理をサポートする必要があります受信パケットのアクセス制御 (MAC) ヘッダー。 ドライバーでは、このサポートをアドバタイズで、次のフラグを設定して、 **SupportedMacHeaderFields**メンバー。

    -   NDIS\_受信\_フィルター\_MAC\_ヘッダー\_DEST\_ADDR\_サポートされています。

    -   NDIS\_受信\_フィルター\_MAC\_ヘッダー\_プロトコル\_サポートされています。

    -   NDIS\_受信\_フィルター\_MAC\_ヘッダー\_パケット\_型\_サポートされています。

    **注**ミニポート ドライバーは、NDIS を設定していない場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ドライバーは、を設定する必要があります**SupportedMacHeaderFields**メンバーをゼロにします。



7.  ミニポート ドライバーの設定、NDIS 場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ミニポート ドライバーが内のデータのフィルター処理をサポートする必要があります、アドレス解決プロトコル (ARP) の受信パケットのヘッダー。 ドライバーでは、このサポートをアドバタイズで、次のフラグを設定して、 **SupportedARPHeaderFields**メンバー。

    -   NDIS\_受信\_フィルター\_ARP\_ヘッダー\_操作\_サポートされています。

    -   NDIS\_受信\_フィルター\_ARP\_ヘッダー\_SPA\_サポートされています。

    -   NDIS\_受信\_フィルター\_ARP\_ヘッダー\_TPA\_サポートされています。

    **注**ミニポート ドライバーは、NDIS を設定していない場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ドライバーは、を設定する必要があります**SupportedARPHeaderFields**メンバーをゼロにします。



8.  ミニポート ドライバーの設定、NDIS 場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ミニポート ドライバーが開く内のデータのフィルター処理をサポートする必要がありますOSI) レイヤー 3 の (L3) ヘッダーを受信した IP バージョン 4 (IPv4) のパケットです。 ドライバーでは、このサポートをアドバタイズで、次のフラグを設定して、 **SupportedIPv4HeaderFields**メンバー。

    -   NDIS\_受信\_フィルター\_IPV4\_ヘッダー\_プロトコル\_サポートされています。

    **注**ミニポート ドライバーは、NDIS を設定していない場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ドライバーは、を設定する必要があります**SupportedIPv4HeaderFields**メンバーをゼロにします。



9.  ミニポート ドライバーの設定、NDIS 場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ミニポート ドライバーが、L3 内のデータのフィルター処理をサポートする必要があります受信 IP version 6 (IPv6) のヘッダー パケット。 ドライバーでは、このサポートをアドバタイズで、次のフラグを設定して、 **SupportedIPv6HeaderFields**メンバー。

    -   NDIS\_受信\_フィルター\_IPV6\_ヘッダー\_プロトコル\_サポートされています。

    **注**ミニポート ドライバーは、NDIS を設定していない場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ドライバーは、を設定する必要があります**SupportedIPv6HeaderFields**メンバーをゼロにします。



10. ミニポート ドライバーの設定、NDIS 場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ミニポート ドライバーは、OSI 内のデータのフィルタ リングをサポートする必要があります受信したユーザー データグラム プロトコル (UDP) パケットの 4 (L4) ヘッダーをレイヤーします。 ドライバーでは、このサポートをアドバタイズで、次のフラグを設定して、 **SupportedIUdpHeaderFields**メンバー。

    -   NDIS\_受信\_フィルター\_UDP\_ヘッダー\_DEST\_ポート\_サポートされています。

    **注**UDP フィルターのテストに失敗した場合、オプションの IPv4 または IPv6 拡張ヘッダーが受信 UDP パケットが含まれる場合、ネットワーク アダプターではパケットを処理できます。 これにより、アダプターは受信したパケットを自動的に削除できます。




**注**ミニポート ドライバーは、NDIS を設定していない場合\_受信\_フィルター\_パケット\_COALESCING\_フィルター\_有効フラグ、ドライバーは、を設定する必要があります**SupportedIUdpHeaderFields**メンバーをゼロにします。




11. ミニポート ドライバーでは、パケット ヘッダー フィールドに指定できる 1 つのパケットの結合フィルターのテストの最大数を報告する必要があります。 ドライバーは、この値を指定します、 **MaxFieldTestsPerPacketCoalescingFilter**メンバー。

    **注**パケットの結合をサポートするネットワーク アダプターが 1 つのパケットの結合フィルターの指定できる 5 つ以上のパケット ヘッダー フィールドをサポートする必要があります。 アダプターがパケットの結合をサポートしていない場合、ミニポート ドライバーは 0 にこの値を設定する必要があります。



12. ミニポート ドライバーでは、ネットワーク アダプターでサポートされているパケット結合フィルターの最大数を報告する必要があります。 ドライバーは、この値を指定します、 **MaxPacketCoalescingFilters**メンバー。

    **注**パケットの結合をサポートするネットワーク アダプターが 10 個以上のパケットの結合フィルターをサポートする必要があります。 アダプターがパケットの結合をサポートしていない場合、ミニポート ドライバーは 0 にこの値を設定する必要があります。



NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数の場合、ドライバーがパケットの結合と基になるネットワーク アダプターの機能をフィルター処理に従うと報告手順:

-   ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

    場合、  **\*PacketCoalescing**キーワード、レジストリ設定は、1、ミニポート ドライバーのセットの値を持つ、 **HardwareReceiveFilterCapabilities**メンバーへのポインターを以前初期化[ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。

    場合、  **\*PacketCoalescing**キーワード、レジストリ設定が 0 の値を持つ、ミニポート ドライバーがパケットの結合のサポートをアドバタイズしません。 設定する必要がありますが、 **HardwareReceiveFilterCapabilities**メンバーを NULL にします。

-   ドライバー呼び出し[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)設定と、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

結合して、基になるネットワーク アダプターの機能をフィルター処理、パケットを報告するミニポート ドライバーによって使用されるメソッドは、電源管理機能を報告するための NDIS 6.20 が動作方法に基づきます。 この方法の詳細については、次を参照してください。[電源管理機能の報告](reporting-power-management-capabilities.md)します。

アダプターの初期化プロセスの詳細については、次を参照してください。[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

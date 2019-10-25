---
title: 仮想スイッチ フィルターの使用
description: 仮想スイッチ フィルターの使用
ms.assetid: 09325037-F9A4-45C8-97E0-8FCA7D42A120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e01ac4535ad541210c46d16bcdae97bffb73457d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842965"
---
# <a name="using-virtual-switch-filtering"></a>仮想スイッチ フィルターの使用

## <a name="overview-of-virtual-switch-filtering"></a>仮想スイッチのフィルター処理の概要

仮想スイッチのフィルター処理は、windows 8 以降のバージョンの Windows でサポートされています。

この WFP 機能では、MAC ヘッダー、IP ヘッダー、および上位プロトコルポートのフィールドに加えて、仮想ポート (VPort) や仮想マシン識別子 (VM ID) などの仮想スイッチ固有のフィールドをフィルター処理できます。 これらのレイヤーは、仮想スイッチを通過するすべてのパケットについて、パケット単位で呼び出されます。 これらのレイヤーには、仮想スイッチ拡張機能フィルター (NDIS ライトウェイトフィルター (LWF) ドライバーの一種) からアクセスします。

コールアウトドライバーは、仮想スイッチレイヤーイベントのコールバックエントリポイントを登録するために[**FwpsvSwitchEventsSubscribe0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventssubscribe0)関数を呼び出します。

コールバック通知関数のエントリポイントは、 [**Fwps\_VSWITCH\_イベント\_ディスパッチ\_TABLE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_vswitch_event_dispatch_table0_)構造体で指定されます。 使用できるコールバック関数は次のとおりです。

* [*FWPS\_VSWITCH\_フィルター\_エンジン\_並べ替え\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_filter_engine_reorder_callback0)
* [*FWPS\_VSWITCH\_インターフェイス\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_interface_event_callback0)
* [*FWPS\_VSWITCH\_有効期間\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_lifetime_event_callback0)
* [*FWPS\_VSWITCH\_ポリシー\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_policy_event_callback0)
* [*FWPS\_VSWITCH\_ポート\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_port_event_callback0)
* [*FWPS\_VSWITCH\_ランタイム\_状態\_復元\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_restore_callback0)
* [*FWPS\_VSWITCH\_ランタイム\_状態\_保存\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_save_callback0)

[**Fwps\_VSWITCH\_イベント\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_vswitch_event_type_)列挙体は、仮想スイッチ通知関数の*eventType*パラメーターの値を定義します。

コールアウトドライバーは、最終的に[**FwpsvSwitchEventsUnsubscribe0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventsunsubscribe0)を呼び出して、システムリソースを解放する必要があります。

コールアウトドライバーによって、WFP 通知機能から保留中の状態\_が返された場合、WFP は、保留中の状態\_を OID 要求ハンドラーに返します。 コールアウトドライバーは、保留中の操作を完了するために[**FwpsvSwitchNotifyComplete0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitchnotifycomplete0)関数を呼び出す必要があります。 **FwpsvSwitchNotifyComplete0**の呼び出しの後、WFP は[**NdisFOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete)関数を呼び出して仮想スイッチの OID を完成させます。

コールバックでは、通知関数のコンテキストで同期的に WFP フィルターを追加または削除することはできません。 また、通知関数によって、コールバックがステータス\_保留中に戻り、コールアウトがステータス\_PENDING を返すことが許可されている場合、通知を完了する前に、コールアウトが WFP フィルターを追加または削除することはできません。

## <a name="wfp-virtual-switch-filter-layer-and-fields"></a>WFP 仮想スイッチフィルターレイヤーとフィールド

仮想スイッチフィルターの[ランタイムフィルターレイヤー識別子](https://docs.microsoft.com/windows-hardware/drivers/network/run-time-filtering-layer-identifiers)には次のものがあります。

* FWPS\_レイヤー\_入口\_VSWITCH\_イーサネット
* FWPS\_レイヤー\_送信\_VSWITCH\_イーサネット
* FWPS\_レイヤー\_受信\_VSWITCH\_トランスポート\_V4
* FWPS\_レイヤー\_入口\_VSWITCH\_TRANSPORT\_V6
* FWPS\_レイヤー\_送信\_VSWITCH\_トランスポート\_V4
* FWPS\_レイヤー\_送信\_VSWITCH\_トランスポート\_V6

仮想スイッチフィルターの[データフィールド識別子](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)には次のものがあります。

* [**FWPS\_のフィールド\_送信\_VSWITCH\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_ethernet_)
* [**FWPS\_フィールド\_送信\_VSWITCH\_トランスポート\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v4_)
* [**FWPS\_フィールド\_送信\_VSWITCH\_トランスポート\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v6_)
* [**FWPS\_フィールド\_受信\_VSWITCH\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_ethernet_)
* [**FWPS\_フィールド\_受信\_VSWITCH\_トランスポート\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v4_)
* [**FWPS\_フィールド\_受信\_VSWITCH\_トランスポート\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v6_)

## <a name="guidance-for-wfp-virtual-switch-callout-writers"></a>WFP 仮想スイッチのコールアウトライターに関するガイダンス

### <a name="port-0-traffic"></a>ポート0のトラフィック

WFP 仮想スイッチのコールアウトの場合、ポート 0 (既定のポート ID) からのトラフィックは信頼されているため、フィルター処理することはできません。 これは、一般に、ポート0経由のトラフィックはドライバースタック内の他の拡張機能から送信されるため、データパスによって privileged および trusted として扱われるためです。 仮想スイッチ拡張機能では、制御パケットの送信など、基になる拡張機能によってフィルター処理および拒否されないような状況では、ポート0を使用することは控えめです。 Hyper-v 拡張可能スイッチのソースポートの詳細については、「[パケットの拡張可能スイッチのソースポートデータを変更する](modifying-a-packet-s-extensible-switch-source-port-data.md)」を参照してください。

### <a name="callout-matching-rules"></a>コールアウト規則

フィルター処理用の照合ルールを定義する場合、仮想スイッチのコールアウトでは、比較の基準として MAC アドレスを使用しないでください。 MAC アドレスは実行時に変更されることがあり、一部のポートでは複数の MAC アドレスからのトラフィックが生成される場合があります。 代わりに、コールアウトは NIC ID などのより持続性のある照合ルールを使用する必要がありますが、これは変更されません。

### <a name="io-virtualization-iov-and-wfp-coexistence"></a>I/o 仮想化 (SR-IOV) と WFP の共存

WFP は、SR-IOV スイッチで有効にすることはできません。有効にしようとすると、OS によってブロックされます。

### <a name="enabling-or-disabling-wfp"></a>WFP の有効化または無効化

WFP 仮想スイッチのコールアウト用インストーラーでは、WFP 拡張が有効になっている状態を変更することはできません。つまり、WFP 自体を有効または無効にすることはできません。




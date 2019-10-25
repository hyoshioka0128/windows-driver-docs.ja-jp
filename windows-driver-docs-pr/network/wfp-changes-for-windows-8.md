---
title: Windows 8 での WFP の変更
description: Windows 8 での WFP の変更
ms.assetid: B83EC5A5-6169-49AB-A7EC-F2078AA0735E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a97281105a6f232a9c12fef45b4247586b07932e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841703"
---
# <a name="wfp-changes-for-windows-8"></a>Windows 8 での WFP の変更


Windows 8 以降では、Windows フィルタリングプラットフォームの使用可能な機能と動作にいくつかの変更が加えられています。 多くの場合、新しい機能を利用するには、NTDDI\_VERSION マクロが NTDDI\_WIN8 に設定されているコールアウトドライバーをコンパイルまたは再コンパイルする必要があります。

-   新機能:
    - [レイヤー2フィルターの使用](using-layer-2-filtering.md)
    - [プロキシ接続の追跡の使用](using-proxied-connections-tracking.md)
    - [仮想スイッチのフィルター処理の使用](using-virtual-switch-filtering.md)
-   新しい関数:
    - [**FwpsCalloutRegister2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister2)
    - [**FwpsFlowAbort0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowabort0)
    - [**FwpsInjectMacReceiveAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacreceiveasync0)
    - [**FwpsInjectMacSendAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacsendasync0)
    - [**FwpsNetBufferListAssociateContext1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext1)
    - [**FwpsQueryConnectionRedirectState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0)
    - [**FwpsRedirectHandleCreate0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)
    - [**FwpsRedirectHandleDestroy0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandledestroy0)
    - [**FwpsvSwitchEventsSubscribe0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventssubscribe0)
    - [**FwpsvSwitchEventsUnsubscribe0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventsunsubscribe0)
    - [**FwpsvSwitchNotifyComplete0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitchnotifycomplete0)
-   新しいコールバック関数:
    - [*FWPS\_コールアウト\_分類\_FN2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn2)
    - [*FWPS\_コールアウト\_通知\_FN2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn2)
    - [*FWPS\_NET\_BUFFER\_LIST\_通知\_FN1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)
    - [*FWPS\_VSWITCH\_フィルター\_エンジン\_並べ替え\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_filter_engine_reorder_callback0)
    - [*FWPS\_VSWITCH\_インターフェイス\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_interface_event_callback0)
    - [*FWPS\_VSWITCH\_有効期間\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_lifetime_event_callback0)
    - [*FWPS\_VSWITCH\_ポリシー\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_policy_event_callback0)
    - [*FWPS\_VSWITCH\_ポート\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_port_event_callback0)
    - [*FWPS\_VSWITCH\_ランタイム\_状態\_復元\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_restore_callback0)
    - [*FWPS\_VSWITCH\_ランタイム\_状態\_保存\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_save_callback0)
-   新しい構造:
    - [**FWPS\_FILTER2**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_filter2_)
    - [**FWPS\_VSWITCH\_イベント\_ディスパッチ\_TABLE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_vswitch_event_dispatch_table0_)
-   新しい列挙型:
    - [**FWPS\_接続\_リダイレクト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_connection_redirect_state_)
    - [**FWPS\_のフィールド\_送信\_VSWITCH\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_ethernet_)
    - [**FWPS\_フィールド\_送信\_VSWITCH\_トランスポート\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v4_)
    - [**FWPS\_フィールド\_送信\_VSWITCH\_トランスポート\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v6_)
    - [**FWPS\_のフィールド\_受信\_MAC\_フレーム\_ネイティブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_native_)
    - [**FWPS\_フィールド\_受信\_VSWITCH\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_ethernet_)
    - [**FWPS\_フィールド\_受信\_VSWITCH\_トランスポート\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v4_)
    - [**FWPS\_フィールド\_受信\_VSWITCH\_トランスポート\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v6_)
    - [**FWPS\_のフィールド\_送信\_MAC\_フレーム\_ネイティブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_native_)
    - [**FWPS\_VSWITCH\_イベント\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_vswitch_event_type_)
-   名前が変更された列挙型:
    - [**Fwps\_のフィールド\_受信\_mac\_フレーム\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_)(Was **FWPS\_フィールド\_受信\_MAC\_フレーム\_802\_3**)
    - [**Fwps\_のフィールド\_送信\_mac\_フレーム\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_)(Was **FWPS\_フィールド\_送信\_MAC\_フレーム\_802\_3**)

 

 






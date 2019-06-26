---
title: Windows 8 での WFP の変更
description: Windows 8 での WFP の変更
ms.assetid: B83EC5A5-6169-49AB-A7EC-F2078AA0735E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d95494fee32ccfb12456e96f72d4ba4f4f6a38e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357028"
---
# <a name="wfp-changes-for-windows-8"></a>Windows 8 での WFP の変更


使用可能な関数と、Windows フィルタ リング プラットフォームを開始する Windows 8 での動作では、いくつかの変更が加えられました。 多くの場合、新しい機能を利用する必要がありますのコンパイル時またはを持つ、NTDDI コールアウト ドライバーを再コンパイル\_バージョン マクロ設定 NTDDI\_WIN8 します。

-   新機能:
    - [レイヤー 2 のフィルターを使用します。](using-layer-2-filtering.md)
    - [追跡プロキシの接続を使用します。](using-proxied-connections-tracking.md)
    - [仮想スイッチのフィルターを使用します。](using-virtual-switch-filtering.md)
-   新しい関数:
    - [**FwpsCalloutRegister2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscalloutregister2)
    - [**FwpsFlowAbort0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsflowabort0)
    - [**FwpsInjectMacReceiveAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectmacreceiveasync0)
    - [**FwpsInjectMacSendAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectmacsendasync0)
    - [**FwpsNetBufferListAssociateContext1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext1)
    - [**FwpsQueryConnectionRedirectState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0)
    - [**FwpsRedirectHandleCreate0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)
    - [**FwpsRedirectHandleDestroy0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsredirecthandledestroy0)
    - [**FwpsvSwitchEventsSubscribe0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsvswitcheventssubscribe0)
    - [**FwpsvSwitchEventsUnsubscribe0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsvswitcheventsunsubscribe0)
    - [**FwpsvSwitchNotifyComplete0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsvswitchnotifycomplete0)
-   新しいコールバック関数:
    - [*FWPS\_コールアウト\_分類\_FN2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn2)
    - [*FWPS\_コールアウト\_通知\_FN2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_notify_fn2)
    - [*FWPS\_NET\_バッファー\_一覧\_通知\_FN1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)
    - [*FWPS\_VSWITCH\_FILTER\_ENGINE\_REORDER\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_vswitch_filter_engine_reorder_callback0)
    - [*FWPS\_VSWITCH\_インターフェイス\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_vswitch_interface_event_callback0)
    - [*FWPS\_VSWITCH\_有効期間\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_vswitch_lifetime_event_callback0)
    - [*FWPS\_VSWITCH\_ポリシー\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_vswitch_policy_event_callback0)
    - [*FWPS\_VSWITCH\_ポート\_イベント\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_vswitch_port_event_callback0)
    - [*FWPS\_VSWITCH\_ランタイム\_状態\_復元\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_restore_callback0)
    - [*FWPS\_VSWITCH\_RUNTIME\_STATE\_SAVE\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_save_callback0)
-   新しい構造体。
    - [**FWPS\_FILTER2**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_filter2_)
    - [**FWPS\_VSWITCH\_イベント\_ディスパッチ\_TABLE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_vswitch_event_dispatch_table0_)
-   新しい列挙体。
    - [**FWPS\_接続\_リダイレクト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_connection_redirect_state_)
    - [**FWPS\_フィールド\_エグレス\_VSWITCH\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_ethernet_)
    - [**FWPS\_フィールド\_エグレス\_VSWITCH\_トランスポート\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v4_)
    - [**FWPS\_FIELDS\_EGRESS\_VSWITCH\_TRANSPORT\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v6_)
    - [**FWPS\_フィールド\_受信\_MAC\_フレーム\_ネイティブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_native_)
    - [**FWPS\_フィールド\_イングレス\_VSWITCH\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_ethernet_)
    - [**FWPS\_フィールド\_イングレス\_VSWITCH\_トランスポート\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v4_)
    - [**FWPS\_FIELDS\_INGRESS\_VSWITCH\_TRANSPORT\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v6_)
    - [**FWPS\_フィールド\_送信\_MAC\_フレーム\_ネイティブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_native_)
    - [**FWPS\_VSWITCH\_イベント\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_vswitch_event_type_)
-   列挙型の名前が変更されました。
    - [**FWPS\_フィールド\_受信\_MAC\_フレーム\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_) (が**FWPS\_フィールド\_受信\_MAC\_フレーム\_802\_3**)
    - [**FWPS\_フィールド\_送信\_MAC\_フレーム\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_) (が**FWPS\_フィールド\_送信\_MAC\_フレーム\_802\_3**)

 

 






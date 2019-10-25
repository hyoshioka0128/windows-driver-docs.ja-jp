---
title: Windows 7 での WFP の変更
description: Windows 7 での WFP の変更
ms.assetid: c7b15182-592a-4cdb-98aa-5283ed2f51a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbb6c495e6f6683261e12e62f123a09dee88206f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841704"
---
# <a name="wfp-changes-for-windows-7"></a>Windows 7 での WFP の変更


Windows 7 以降では、Windows フィルタリングプラットフォームの使用可能な機能と動作にいくつかの変更が加えられています。 多くの場合、新しい機能を利用するには、NTDDI\_VERSION マクロが NTDDI\_WIN7 に設定されているコールアウトドライバーをコンパイルまたは再コンパイルする必要があります。

-   新しい関数:
    - [**FwpsAcquireClassifyHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquireclassifyhandle0)
    - [**FwpsAcquireWritableLayerDataPointer0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquirewritablelayerdatapointer0)
    - [**FwpsApplyModifiedLayerData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsapplymodifiedlayerdata0)
    - [**FwpsCalloutRegister1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister1)
    - [**FwpsCompleteClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteclassify0)
    - [**FwpsPendClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0)
    - [**FwpsReleaseClassifyHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreleaseclassifyhandle0)
    - [*classifyFn1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn1)
    - [*notifyFn1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn1)
    - [**FWPS\_NET\_BUFFER\_LIST\_通知\_FN0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)
    - [**FwpsInjectTransportSendAsync1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportsendasync1)
    - [**FwpsNetBufferListAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext0)
    - [**FwpsNetBufferListGetTagForContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistgettagforcontext0)
    - [**FwpsNetBufferListRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)
    - [**FwpsNetBufferListRetrieveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0)
    - [**FwpsAleEndpointCreateEnumHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointcreateenumhandle0)
    - [**FwpsAleEndpointDestroyEnumHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointdestroyenumhandle0)
    - [**FwpsAleEndpointEnum0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointenum0)
    - [**FwpsAleEndpointGetById0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointgetbyid0)
    - [**FwpsAleEndpointGetSecurityInfo0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointgetsecurityinfo0)
    - [**FwpsAleEndpointSetSecurityInfo0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointsetsecurityinfo0)
-   新しい構造体と列挙型:
    - [**FWPS\_ALE\_エンドポイント\_列挙型\_TEMPLATE0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_ale_endpoint_enum_template0_)
    - [**FWPS\_ALE\_エンドポイント\_PROPERTIES0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_ale_endpoint_properties0_)
    - [**FWPS\_バインド\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_bind_request0)
    - [**FWPS\_CALLOUT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout1_)
    - [**FWPS\_CONNECT\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)
    - [**FWPS\_フィールド\_ALE\_バインド\_リダイレクト\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_bind_redirect_v4_)
    - [**FWPS\_フィールド\_ALE\_バインド\_リダイレクト\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_bind_redirect_v6_)
    - [**FWPS\_フィールド\_ALE\_接続\_リダイレクト\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_connect_redirect_v4_)
    - [**FWPS\_フィールド\_ALE\_接続\_リダイレクト\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_connect_redirect_v6_)
    - [**FWPS\_フィールド\_ALE\_エンドポイント\_クロージャ\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_endpoint_closure_v4_)
    - [**FWPS\_フィールド\_ALE\_エンドポイント\_クロージャ\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_endpoint_closure_v6_)
    - [**FWPS\_フィールド\_ALE\_リソース\_リリース\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_resource_release_v4_)
    - [**FWPS\_フィールド\_ALE\_リソース\_リリース\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_resource_release_v6_)
    - [**FWPS\_のフィールド\_受信\_MAC\_フレーム\_802\_3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_)
    - [**FWPS\_フィールド\_KM\_認証**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_km_authorization_)
    - [**FWPS\_フィールド\_名前\_解決\_キャッシュ\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_name_resolution_cache_v4_)
    - [**FWPS\_フィールド\_名前\_解決\_キャッシュ\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_name_resolution_cache_v6_)
    - [**FWPS\_フィールド\_送信\_MAC\_フレーム\_802\_3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_)
    - [**FWPS\_フィールド\_ストリーム\_パケット\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_stream_packet_v4_)
    - [**FWPS\_のフィールド\_ストリーム\_パケット\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_stream_packet_v6_)
    - [**FWPS\_FILTER1**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_filter1_)
    - [**FWPS\_NET\_BUFFER\_LIST\_イベント\_TYPE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_net_buffer_list_event_type0_)
    - [**FWPS\_TRANSPORT\_SEND\_PARAMS1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_transport_send_params1_)
-   新しいドキュメントのトピック:
    - [バインドまたは接続リダイレクトの使用](using-bind-or-connect-redirection.md)
    - [パケットタグ付けの使用](using-packet-tagging.md)
    - [ALE エンドポイントの有効期間の管理](ale-endpoint-lifetime-management.md)

 

 






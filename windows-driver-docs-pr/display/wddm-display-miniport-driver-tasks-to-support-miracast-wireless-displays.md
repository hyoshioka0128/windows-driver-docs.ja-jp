---
title: WDDM ワイヤレスディスプレイのミニポートドライバーのサポートを表示する
description: Miracast ワイヤレスディスプレイをサポートするために、Windows Display Driver Model (WDDM) では、カーネルモードで実行されるミニポートドライバーが、次のタスクを実行する必要があります。
ms.assetid: D67CAC4F-0409-4E8D-A31A-78C3EB473556
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: d99e4b37829f5afe73990a5331f44501a2edc2df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825230"
---
# <a name="wddm-display-miniport-driver-tasks-to-support-miracast-wireless-displays"></a>Miracast ワイヤレス ディスプレイをサポートする WDDM ディスプレイ ミニポート ドライバーのタスク


Miracast ワイヤレスディスプレイをサポートするために、Windows Display Driver Model (WDDM) では、カーネルモードで実行されるミニポートドライバーが、次のタスクを実行する必要があります。

## <a name="supporting-the-miracast-interface"></a>Miracast インターフェイスのサポート


ディスプレイミニポートドライバーが Miracast の表示をサポートしている場合は、 [**DXGK\_miracast\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_miracast_interface)を報告する必要があります。これには、ドライバーによって実装された miracast 関数へのポインターが含まれています (Microsoft DirectX グラフィックスの場合)。カーネルサブシステムは、 [*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数を呼び出します。

オペレーティングシステムの DirectX グラフィックカーネルサブシステム (Dxgkrnl) が、Miracast 表示インターフェイスのクエリを実行するために[*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数を呼び出していない場合、miracast ワイヤレスディスプレイ、およびディスプレイミニポートドライバーをサポートしていません。Miracast ターゲットを報告しません。

ドライバーは、完全な WDDM グラフィックスデバイスに複数の Miracast ターゲットを報告しないようにする必要があります。そうしないと、オペレーティングシステムはアダプターを起動できません。

Dxgkrnl が[*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)を呼び出して Miracast 表示インターフェイスを照会した後、Dxgkrnl が[*DxgkDdiQueryChildRelations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)関数を呼び出したときに、デバイスの初期化中に、ドライバーはターゲットの種類を**D3DKMDT\_vot\_Miracast**として報告できます。

Miracast ターゲットは、Dxgkrnl が Miracast 接続セッションを開始するまで、disconnected 状態のままにしておく必要があります。 Miracast セッションが開始され、モニターが Miracast シンクに接続されている場合、または新しいモニターが Miracast シンクに接続しているためにドライバーが Miracast ユーザーモードドライバーから i/o 要求を受信した場合、ディスプレイミニポートドライバーはモニターを報告する必要があります。[**DxgkCbIndicateChildStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status)関数を呼び出すことにより、オペレーティングシステムに対してホットプラグ検出 (hpd) の認識値が到着します。 この呼び出しでは、ドライバーは次の値を設定する必要があります。

| [**DXGK\_子\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_status)メンバー | Value                                                                                                                                                                                                                                                                      |
|-------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Type**                                                    | [**DXGK\_CHILD\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ne-dispmprt-_dxgk_child_status_type)の**statusmiracast**定数値\_TYPE 列挙型                                                                                                                                                       |
| **Miracast**。**接続済み**                                  | **TRUE**                                                                                                                                                                                                                                                                   |
| **Miracast**。**MiracastMonitorType**                        | 接続の種類を示す値です。 Miracast シンクがモニターまたはテレビに埋め込まれている場合は、 [**D3DKMDT\_VIDEO\_出力\_テクノロジ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)列挙の**D3DKMDT\_VOT\_Miracast**定数値に設定する必要があります。 |

 

表示ミニポートドライバーが実装する Miracast 関数は次のとおりです。

<span id="DxgkDdiMiracastCreateContext"></span><span id="dxgkddimiracastcreatecontext"></span><span id="DXGKDDIMIRACASTCREATECONTEXT"></span>[*DxgkDdiMiracastCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)  
Miracast 表示デバイスのカーネルモードインスタンスを開始するためのコンテキストを作成します。

<span id="DxgkDdiMiracastDestroyContext"></span><span id="dxgkddimiracastdestroycontext"></span><span id="DXGKDDIMIRACASTDESTROYCONTEXT"></span>[*DxgkDdiMiracastDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)  
Miracast 表示デバイスのカーネルモードインスタンスを開始するためのコンテキストを作成します。

<span id="DxgkDdiMiracastIoControl"></span><span id="dxgkddimiracastiocontrol"></span><span id="DXGKDDIMIRACASTIOCONTROL"></span>[*DxgkDdiMiracastIoControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)  
Miracast ユーザーモードドライバーの呼び出しから[**MiracastIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)への同期 i/o 要求を処理します。

<span id="DxgkDdiMiracastQueryCaps"></span><span id="dxgkddimiracastquerycaps"></span><span id="DXGKDDIMIRACASTQUERYCAPS"></span>[*DxgkDdiMiracastQueryCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps)  
現在のディスプレイアダプターの Miracast 機能に対してクエリを行います。

## <a name="span-idmiracast_session_startspanspan-idmiracast_session_startspanspan-idmiracast_session_startspanmiracast-session-start"></a><span id="Miracast_session_start"></span><span id="miracast_session_start"></span><span id="MIRACAST_SESSION_START"></span>Miracast セッションの開始


Miracast セッションが開始されると、オペレーティングシステムは[*DxgkDdiQueryChildStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)関数を呼び出します。 ディスプレイミニポートドライバーでは、 [**DXGK\_子\_ステータス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_status)に設定する必要があります。 **「** **Statusmiracast** 」と入力し、 **DXGK\_child\_STATUS**の**Miracast**子構造体を使用する必要があります。 モニターが Miracast シンクに接続されている場合、ドライバーは**miracast**を設定する必要があります。**D3DKMDT\_VOT\_MIRACAST**に**接続**しました。

ドライバーでは、 [**D3DKMDT\_VIDEO\_SIGNAL\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)の値を指定する必要があります。**Vsyncfreqdivider**。 miracast 接続されたセッションを通じて miracast シンクの垂直の割合に表示されるモニターの垂直速度の比率です。 たとえば、Miracast シンクの垂直リフレッシュ率が 240 Hz で、接続されたディスプレイの垂直方向の割り込み頻度が 30 Hz の場合、ドライバーは**Vsyncfreqdivider**を8に設定する必要があります。

## <a name="span-idhandling_interrupts_for_completed_encode_chunksspanspan-idhandling_interrupts_for_completed_encode_chunksspanspan-idhandling_interrupts_for_completed_encode_chunksspanhandling-interrupts-for-completed-encode-chunks"></a><span id="Handling_interrupts_for_completed_encode_chunks"></span><span id="handling_interrupts_for_completed_encode_chunks"></span><span id="HANDLING_INTERRUPTS_FOR_COMPLETED_ENCODE_CHUNKS"></span>完了したエンコードチャンクの割り込みの処理


ワイヤレス Miracast 接続を介して送信される1つのフレームのデータは、1つまたは複数のエンコードチャンクに分割できます。 GPU がこれらのチャンクの1つのエンコードを完了するたびに、割り込みを生成する必要があります。 この割り込みに対する応答として、ディスプレイミニポートドライバーは、 [*Dxgkcbnotifyinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt)関数を呼び出し、Dxgkargcb で**MiracastEncodeChunkCompleted**子構造体を完了する必要があります。これは、 [ **\_割り込み\_通知\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data)構造。 [**DXGK\_INTERRUPT\_type**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_interrupt_type) Interrupt type を**DXGK\_interrupt\_MICACAST\_CHUNK\_PROCESSING\_COMPLETE**に設定します。

割り込み処理の一部として、ドライバーは必要に応じて**MiracastEncodeChunkCompleted**を指定できます。[**Dxgkargcb\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data)の**Pprivatedriverdata**および**Privatedatadriversize**メンバーは、\_割り込み\_データ構造に通知します。 ユーザーモードドライバーは、 [**MIRACAST\_チャンク\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_data)内のこのプライベートドライバーデータにアクセスできます。**Privatedriverdata**メンバー。

一定期間にわたってディスプレイミニポートドライバーが、ユーザーモードのディスプレイドライバーが使用するよりも多くのパケットをチャンクデータで生成する場合は、新しいチャンクに使用できる空きメモリ領域が不足する可能性があります。この場合、ディスプレイミニポートドライバーは、 **MiracastEncodeChunkCompleted**で **\_\_メモリなしのステータス**を返します。**ステータス**。これは、オペレーティングシステムの GPU スケジューラにエラー状態を通知するために、 [*Dxgkcbnotifydpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_dpc)関数を呼び出す必要があります。 [**GetNextChunkData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)関数を呼び出すと、状態コードの**リセット\_状態\_** が返され、その後の呼び出しではリセット操作後に送信されたチャンクの受信が開始されます。 一部のチャンクは失われているため、ドライバーで新しい I フレームを生成して送信することをお勧めします。

## <a name="span-idrestrictions_on_source_modesspanspan-idrestrictions_on_source_modesspanspan-idrestrictions_on_source_modesspanrestrictions-on-source-modes"></a><span id="Restrictions_on_source_modes"></span><span id="restrictions_on_source_modes"></span><span id="RESTRICTIONS_ON_SOURCE_MODES"></span>ソースモードに関する制限事項


WDDM 表示ミニポートドライバーは、ピクセルパイプラインの制約を処理するために、通常、オペレーティングシステムに公開されているソースモードを制限します。 ドライバーは、ピクセルパイプラインでもサポートされているモニターによって公開されているモードでソースモードの一覧を作成するだけで、これを行います。 たとえば、ドライバーは、ピクセルパイプラインの制約に基づいて EDID を変更しません。

同様に、Miracast の場合は、ソースモードとターゲットモードのセットを列挙するときに、オペレーティングシステムに公開されているソースモードのセットが、ミニポートドライバーによって制限されます。 Miracast の場合、GPU エンコード機能、ネットワークプロパティ、およびシンクデコード機能を使用すると、Miracast ピクセルパイプラインがサポートできるソースモードの数を減らすことができます。

ディスプレイミニポートドライバーが[*DXGK\_VIDPNSOURCEMODESET\_INTERFACE::P fnaddmode*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode)関数を呼び出して、Miracast ターゲットに接続されているソースに3d ステレオモードを追加しようとすると、関数の呼び出しは失敗します。

## <a name="span-idcalling_operating_system-provided_callback_functionsspanspan-idcalling_operating_system-provided_callback_functionsspanspan-idcalling_operating_system-provided_callback_functionsspancalling-operating-system-provided-callback-functions"></a><span id="Calling_operating_system-provided_callback_functions"></span><span id="calling_operating_system-provided_callback_functions"></span><span id="CALLING_OPERATING_SYSTEM-PROVIDED_CALLBACK_FUNCTIONS"></span>オペレーティングシステムが提供するコールバック関数の呼び出し


次に示すのは、オペレーティングシステムが提供する Miracast カーネルモードのコールバック関数です。

<span id="DxgkCbMiracastSendMessage"></span><span id="dxgkcbmiracastsendmessage"></span><span id="DXGKCBMIRACASTSENDMESSAGE"></span>[**DxgkCbMiracastSendMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)  
ユーザーモードの表示ドライバーに非同期メッセージを送信します。

<span id="DxgkCbMiracastSendMessageCallback"></span><span id="dxgkcbmiracastsendmessagecallback"></span><span id="DXGKCBMIRACASTSENDMESSAGECALLBACK"></span>[**DxgkCbMiracastSendMessageCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)  
[**DxgkCbMiracastSendMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)の呼び出しで、完了した IRP の[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造を指定するために使用されます。

<span id="DxgkCbReportChunkInfo"></span><span id="dxgkcbreportchunkinfo"></span><span id="DXGKCBREPORTCHUNKINFO"></span>[**DxgkCbReportChunkInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)  
エンコードチャンクに関する情報を報告します。

## <a name="span-idsending_messages_asynchronously_from_kernel-mode_to_user-modespanspan-idsending_messages_asynchronously_from_kernel-mode_to_user-modespanspan-idsending_messages_asynchronously_from_kernel-mode_to_user-modespansending-messages-asynchronously-from-kernel-mode-to-user-mode"></a><span id="Sending_messages_asynchronously_from_kernel-mode_to_user-mode"></span><span id="sending_messages_asynchronously_from_kernel-mode_to_user-mode"></span><span id="SENDING_MESSAGES_ASYNCHRONOUSLY_FROM_KERNEL-MODE_TO_USER-MODE"></span>カーネルモードからユーザーモードにメッセージを非同期的に送信する


表示ミニポートドライバーが、 [*DxgkCbMiracastSendMessage*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)関数を呼び出すときに、関連付けられたユーザーモードドライバーに送信されるメッセージは、Miracast 接続セッションが開始されるまで配信されません。 したがって、ユーザーモードドライバーの[*StartMiracastSession*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session)関数がまだ呼び出されていない場合、送信されたメッセージは*StartMiracastSession*が返されるまで遅延されます。 [*StopMiracastSession*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)関数が呼び出された後にメッセージが送信された場合、オペレーティングシステムによってメッセージが削除され、 [*DxgkCbMiracastSendMessageCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)関数は、 *piostatusblock*で設定されたエラー状態で呼び出されます。&gt;の**状態**を-します。

## <a name="span-idmodifying_an_existing_display_miniport_driver_to_support_miracast_displaysspanspan-idmodifying_an_existing_display_miniport_driver_to_support_miracast_displaysspanspan-idmodifying_an_existing_display_miniport_driver_to_support_miracast_displaysspanmodifying-an-existing-display-miniport-driver-to-support-miracast-displays"></a><span id="Modifying_an_existing_display_miniport_driver_to_support_Miracast_displays"></span><span id="modifying_an_existing_display_miniport_driver_to_support_miracast_displays"></span><span id="MODIFYING_AN_EXISTING_DISPLAY_MINIPORT_DRIVER_TO_SUPPORT_MIRACAST_DISPLAYS"></span>既存の表示ミニポートドライバーを変更して Miracast の表示をサポートする


[*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)関数が呼び出されると、ディスプレイミニポートドライバーは、新しい Miracast ターゲットを追加する必要があり、ターゲットのホットプラグ検出 (hpd) 認識値を**HpdAwarenessInterruptible**としてマークして、オペレーティングシステムがこのターゲットをポーリングしません。 また、 [*DxgkDdiQueryChildRelations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)関数が呼び出されると、ドライバーは、接続の種類として**D3DKMDT\_VOT\_MIRACAST**を報告する必要があります。

ドライバーは、完全な WDDM グラフィックスデバイスに複数の Miracast ターゲットを報告しないでください。 ドライバーが複数の Miracast ターゲットを報告する場合、オペレーティングシステムはアダプターの起動に失敗します。 また、Miracast 接続セッションが開始されていない場合、このターゲットのモニターを報告しないようにする必要があります。

また、ドライバーは、DirectX グラフィックスカーネルサブシステムが[*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数を呼び出したときに、カーネルモードアドレス空間にある関数へのポインターを使用して、正しい[**DXGK\_MIRACAST\_表示\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_miracast_interface)構造を報告する必要もあります。

Miracast セッションが開始され、モニターが Miracast シンクに接続されると、ディスプレイミニポートドライバーは、 [**DXGK\_子\_ステータス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_status)を設定する必要があります。**Statusmiracast**定数値に「member」と**入力**します。また、 **DXGK\_CHILD\_STATUS**にも設定する必要があります。**Miracast**。モニターの到着をオペレーティングシステムに報告するために、 **TRUE**に**接続**しました。 ドライバーは、 **DXGK\_子\_ステータス**を設定する必要があります。**Miracast**。**MiracastMonitorType**メンバーは、シンクに接続されている適切なモニターの種類にメンバーをします。 シンクがモニターの一部である場合は、このメンバーを**D3DKMDT\_VOT\_MIRACAST**に設定する必要があります。

ドライバーがモニターの EDID を認識している場合は、オペレーティングシステムが[*DxgkDdiQueryDeviceDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)関数を呼び出したときに、この edid を報告する必要があります。

ハードウェアの機能、Miracast シンクモードの一覧、およびネットワーク帯域幅に応じて、ドライバーは正しいソースモード、ターゲットモード、ローテーションモード、およびスケーリングモードを報告する必要があります。 ターゲットモードの場合、ドライバーは、 [**D3DKMDT\_VIDEO\_SIGNAL\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)に正しい**Vsyncfreqdivider**メンバーの値を報告する必要があります。 オペレーティングシステムは、ターゲットモードをモニターモードと照合し、モニターでサポートされていないモードを排除します。

 

 






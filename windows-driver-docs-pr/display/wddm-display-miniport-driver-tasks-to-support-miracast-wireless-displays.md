---
title: ワイヤレス ディスプレイ WDDM 表示ミニポート ドライバーのサポート
description: Miracast ワイヤレス表示、Windows 表示 Driver Model (WDDM) カーネル モードで実行されているミニポート ドライバーの表示をサポートするためには、次のタスクを実行する必要があります。
ms.assetid: D67CAC4F-0409-4E8D-A31A-78C3EB473556
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: ba4383daec6b83061541b323b378541c64b9433d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376122"
---
# <a name="wddm-display-miniport-driver-tasks-to-support-miracast-wireless-displays"></a>Miracast ワイヤレス ディスプレイをサポートする WDDM ディスプレイ ミニポート ドライバーのタスク


Miracast ワイヤレス表示、Windows 表示 Driver Model (WDDM) カーネル モードで実行されているミニポート ドライバーの表示をサポートするためには、次のタスクを実行する必要があります。

## <a name="supporting-the-miracast-interface"></a>Miracast インターフェイスをサポートしています。


これを報告する必要があるかどうか、ディスプレイのミニポート ドライバーは Miracast 表示をサポートする、 [ **DXGK\_MIRACAST\_表示\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_interface)ポインターを持つ構造体ドライバー実装 Miracast 関数に、Microsoft DirectX グラフィックスのカーネルのサブシステムを呼び出すと、 [ *DxgkDdiQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数。

オペレーティング システムの DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) が要求されていない場合、 [ *DxgkDdiQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface) Miracast を照会する関数はサポートしていませんし、インターフェイスを表示Miracast ワイヤレス表示、および表示のミニポート ドライバーは、どの Miracast ターゲットを報告する必要があります。

ドライバーは、完全な WDDM グラフィックス、あらゆるデバイスでそれ以外の場合、アダプターを開始するオペレーティング システムが失敗した Miracast の 1 つ以上のターゲットを報告しない必要があります。

Dxgkrnl 呼び出し後[ *DxgkDdiQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)を Miracast 表示インターフェイスを照会するには、ドライバーとターゲットの種類を報告**D3DKMDT\_VOT\_MIRACAST** Dxgkrnl を呼び出すと、デバイスの初期化中に、 [ *DxgkDdiQueryChildRelations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)関数。

Miracast ターゲットは必要があります、Miracast にセッションが接続されている Dxgkrnl 開始まで、切断状態に残ります。 Miracast セッションを開始すると、し、モニターが Miracast シンクに接続されている、または Miracast シンクに新しいモニターが接続されているため、ドライバーが、Miracast ユーザー モード ドライバーから I/O 要求を受信、ときにディスプレイのミニポート ドライバーは、モニターを報告する必要があります。呼び出すことによって、オペレーティング システムに到着ホットプラグ検出 (HPD) 認識値、 [ **DxgkCbIndicateChildStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status)関数。 この呼び出しで、ドライバーは、これらの値を設定する必要があります。

| [**DXGK\_子\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_status)メンバー | Value                                                                                                                                                                                                                                                                      |
|-------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **型**                                                    | **StatusMiracast**の定数値、 [ **DXGK\_子\_状態\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ne-dispmprt-_dxgk_child_status_type)列挙型                                                                                                                                                       |
| **Miracast**.**接続されています。**                                  | **TRUE**                                                                                                                                                                                                                                                                   |
| **Miracast**.**MiracastMonitorType**                        | 接続の種類を示す値。 これに設定するモニターまたはテレビでは、Miracast シンクが埋め込まれている場合、 **D3DKMDT\_VOT\_MIRACAST**の定数値、 [ **D3DKMDT\_ビデオ\_出力\_テクノロジ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)列挙体。 |

 

これらは、ディスプレイのミニポート ドライバーを実装する Miracast 関数です。

<span id="DxgkDdiMiracastCreateContext"></span><span id="dxgkddimiracastcreatecontext"></span><span id="DXGKDDIMIRACASTCREATECONTEXT"></span>[*DxgkDdiMiracastCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)  
Miracast ディスプレイ デバイスのカーネル モードのインスタンスを起動するコンテキストを作成します。

<span id="DxgkDdiMiracastDestroyContext"></span><span id="dxgkddimiracastdestroycontext"></span><span id="DXGKDDIMIRACASTDESTROYCONTEXT"></span>[*DxgkDdiMiracastDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)  
Miracast ディスプレイ デバイスのカーネル モードのインスタンスを起動するコンテキストを作成します。

<span id="DxgkDdiMiracastIoControl"></span><span id="dxgkddimiracastiocontrol"></span><span id="DXGKDDIMIRACASTIOCONTROL"></span>[*DxgkDdiMiracastIoControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)  
Miracast ユーザー モード ドライバー呼び出しから発信された同期 I/O 要求を処理する[ **MiracastIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)します。

<span id="DxgkDdiMiracastQueryCaps"></span><span id="dxgkddimiracastquerycaps"></span><span id="DXGKDDIMIRACASTQUERYCAPS"></span>[*DxgkDdiMiracastQueryCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps)  
現在のディスプレイ アダプターの Miracast 機能を照会します。

## <a name="span-idmiracastsessionstartspanspan-idmiracastsessionstartspanspan-idmiracastsessionstartspanmiracast-session-start"></a><span id="Miracast_session_start"></span><span id="miracast_session_start"></span><span id="MIRACAST_SESSION_START"></span>Miracast セッションの開始


Miracast セッションが開始されると、オペレーティング システムの呼び出し、 [ *DxgkDdiQueryChildStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_status)関数。 ディスプレイのミニポート ドライバーを設定する必要があります[ **DXGK\_子\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_status).**型**の値に**StatusMiracast**および使用する必要があります、 **Miracast**で子構造**DXGK\_子\_の状態**. ドライバーを設定する必要がありますをモニターを Miracast シンクに接続すると、場合**Miracast**.**接続されている**に**D3DKMDT\_VOT\_MIRACAST**します。

ドライバーの値を指定する必要があります[ **D3DKMDT\_ビデオ\_信号\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info).**VsyncFreqDivider**、Miracast シンクの垂直同期レートにセッションを接続、Miracast を表示するモニターの垂直同期レートの比率します。 たとえば、Miracast シンクの垂直方向のリフレッシュ レートが 240 Hz で接続されているディスプレイの垂直同期割り込み頻度が 30 Hz の場合、ドライバー設定する必要があります**VsyncFreqDivider** 8。

## <a name="span-idhandlinginterruptsforcompletedencodechunksspanspan-idhandlinginterruptsforcompletedencodechunksspanspan-idhandlinginterruptsforcompletedencodechunksspanhandling-interrupts-for-completed-encode-chunks"></a><span id="Handling_interrupts_for_completed_encode_chunks"></span><span id="handling_interrupts_for_completed_encode_chunks"></span><span id="HANDLING_INTERRUPTS_FOR_COMPLETED_ENCODE_CHUNKS"></span>完了、割り込みを処理チャンク エンコード


Miracast ワイヤレス接続経由で転送される 1 つのフレームにデータを 1 つに分割またはチャンク エンコードの詳細はします。 たびに、GPU では、これらのチャンクのいずれかのエンコードが完了すると、割り込みを生成する必要があります。 この割り込みに応答して、ディスプレイのミニポート ドライバーを呼び出す必要があります、 [ *DxgkCbNotifyInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt)関数し、完了、 **MiracastEncodeChunkCompleted**子構造体、 [ **DXGKARGCB\_通知\_INTERRUPT\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data)構造体の設定を含む、 [ **DXGK\_割り込み\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_interrupt_type)割り込みをタイプ**DXGK\_割り込み\_MICACAST\_チャンク\_処理\_完了**します。

ドライバーを必要に応じて指定する、割り込み処理の一環として、 **MiracastEncodeChunkCompleted**.**pPrivateDriverData**と**PrivateDataDriverSize**内のメンバー、 [ **DXGKARGCB\_通知\_INTERRUPT\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data)構造体。 ユーザー モード ドライバーがの場合は、このドライバーのプライベート データにアクセスできる、 [ **MIRACAST\_チャンク\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_data).**PrivateDriverData**メンバー。

時間の期間は、ディスプレイのミニポート ドライバーがよりもデータをチャンクでより多くのパケットを生成する場合は、ユーザー モードのディスプレイ ドライバーを消費する新しいチャンクの使用可能な空きメモリ容量実行できます。この場合、ディスプレイのミニポート ドライバーを返します**状態\_いいえ\_メモリ**で**MiracastEncodeChunkCompleted**.**状態**、呼び出す必要があり、 [ *DxgkCbNotifyDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_dpc)エラー状態について、オペレーティング システムの GPU のスケジューラに通知します。 呼び出し、 [ **GetNextChunkData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)関数は、**状態\_接続\_リセット**ステータス コード、および後続の呼び出しはリセット操作の後に送信されたチャンクの受信を開始します。 一部のチャンクは失われている、ため、ドライバーを生成して、新しい I フレームを送信ことお勧めします。

## <a name="span-idrestrictionsonsourcemodesspanspan-idrestrictionsonsourcemodesspanspan-idrestrictionsonsourcemodesspanrestrictions-on-source-modes"></a><span id="Restrictions_on_source_modes"></span><span id="restrictions_on_source_modes"></span><span id="RESTRICTIONS_ON_SOURCE_MODES"></span>ソース モードに関する制限事項


通常、WDDM ディスプレイ ミニポート ドライバー、ピクセルのパイプラインの制約を処理するためには、オペレーティング システムに公開されているソース モードを制限します。 ドライバーはこれのみピクセルのパイプラインをサポートするモニターによって公開されているモードとソース モードの一覧を作成します。 たとえば、ドライバーは、ピクセルのパイプラインの制約に基づく EDID を変更されません。

同様に、Miracast 表示のディスプレイのミニポート ドライバーのセットを制限は公開されているソース モード オペレーティング システムにソースとターゲットのモードのセットを列挙したとき。 Miracast が表示されます、GPU のエンコード機能、ネットワークのプロパティとシンクのデコード機能は、Miracast ピクセルのパイプラインをサポートできるソース モードの数を減らすことができます。

ディスプレイのミニポート ドライバーを呼び出す場合、 [ *DXGK\_VIDPNSOURCEMODESET\_INTERFACE::pfnAddMode* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode)に接続されているソースを 3-D ステレオ モードを追加しようとする関数をMiracast ターゲットでは、関数呼び出しは失敗します。

## <a name="span-idcallingoperatingsystem-providedcallbackfunctionsspanspan-idcallingoperatingsystem-providedcallbackfunctionsspanspan-idcallingoperatingsystem-providedcallbackfunctionsspancalling-operating-system-provided-callback-functions"></a><span id="Calling_operating_system-provided_callback_functions"></span><span id="calling_operating_system-provided_callback_functions"></span><span id="CALLING_OPERATING_SYSTEM-PROVIDED_CALLBACK_FUNCTIONS"></span>オペレーティング システムで指定されたコールバック関数の呼び出し


これらは、オペレーティング システムを提供する Miracast カーネル モードのコールバック関数です。

<span id="DxgkCbMiracastSendMessage"></span><span id="dxgkcbmiracastsendmessage"></span><span id="DXGKCBMIRACASTSENDMESSAGE"></span>[**DxgkCbMiracastSendMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)  
ユーザー モードのディスプレイ ドライバーには、非同期メッセージを送信します。

<span id="DxgkCbMiracastSendMessageCallback"></span><span id="dxgkcbmiracastsendmessagecallback"></span><span id="DXGKCBMIRACASTSENDMESSAGECALLBACK"></span>[**DxgkCbMiracastSendMessageCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)  
呼び出しで使用される[ **DxgkCbMiracastSendMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)を指定する、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)完了した IRP の構造体。

<span id="DxgkCbReportChunkInfo"></span><span id="dxgkcbreportchunkinfo"></span><span id="DXGKCBREPORTCHUNKINFO"></span>[**DxgkCbReportChunkInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)  
エンコード、チャンクに関する情報を報告します。

## <a name="span-idsendingmessagesasynchronouslyfromkernel-modetouser-modespanspan-idsendingmessagesasynchronouslyfromkernel-modetouser-modespanspan-idsendingmessagesasynchronouslyfromkernel-modetouser-modespansending-messages-asynchronously-from-kernel-mode-to-user-mode"></a><span id="Sending_messages_asynchronously_from_kernel-mode_to_user-mode"></span><span id="sending_messages_asynchronously_from_kernel-mode_to_user-mode"></span><span id="SENDING_MESSAGES_ASYNCHRONOUSLY_FROM_KERNEL-MODE_TO_USER-MODE"></span>ユーザー モードのカーネル モードから非同期的にメッセージの送信


ディスプレイのミニポート ドライバーを呼び出すときにその関連付けられているユーザー モード ドライバーに送信されたメッセージ、 [ *DxgkCbMiracastSendMessage* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)関数は、Miracast セッションを接続するまで配信されません開始されました。 そのため場合、ユーザー モード ドライバーの[ *StartMiracastSession* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session)関数が呼び出されていない、まで、送信されたメッセージを延期*StartMiracastSession*を返します。 後にメッセージが送信される場合、 [ *StopMiracastSession* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)関数が呼び出されると、その後、メッセージは、オペレーティング システムによって削除、および[ *DxgkCbMiracastSendMessageCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)関数を呼び出すとエラー状態の設定*pIoStatusBlock*-&gt;**状態**.

## <a name="span-idmodifyinganexistingdisplayminiportdrivertosupportmiracastdisplaysspanspan-idmodifyinganexistingdisplayminiportdrivertosupportmiracastdisplaysspanspan-idmodifyinganexistingdisplayminiportdrivertosupportmiracastdisplaysspanmodifying-an-existing-display-miniport-driver-to-support-miracast-displays"></a><span id="Modifying_an_existing_display_miniport_driver_to_support_Miracast_displays"></span><span id="modifying_an_existing_display_miniport_driver_to_support_miracast_displays"></span><span id="MODIFYING_AN_EXISTING_DISPLAY_MINIPORT_DRIVER_TO_SUPPORT_MIRACAST_DISPLAYS"></span>Miracast 表示をサポートするために既存のディスプレイ ミニポート ドライバーを変更します。


ときに、 [ *DxgkDdiStartDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)関数が呼び出されると場合、ディスプレイのミニポート ドライバーは新しい Miracast ターゲットを追加する必要があるとターゲットのホットプラグ検出(HPD)認識の値をマークする必要があります**HpdAwarenessInterruptible**オペレーティング システムがこのターゲットをポーリングしないようにします。 また、ときに、 [ *DxgkDdiQueryChildRelations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)関数が呼び出されると、ドライバーを報告する必要があります**D3DKMDT\_VOT\_MIRACAST**としてその接続の種類。

ドライバーは、完全な WDDM グラフィックス デバイスで Miracast の 1 つ以上のターゲットを報告しない必要があります。 ドライバーでは、1 つ以上の Miracast ターゲットを報告する場合、オペレーティング システムは、アダプターの開始に失敗します。 ドライバーでは、Miracast にセッションが接続されている場合は、このターゲットのいずれかのモニターが開始されていないはしないレポートもする必要があります。

また、ドライバーを適切なレポートが必要な[ **DXGK\_MIRACAST\_表示\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_interface)構造は、カーネル モードになっている関数へのポインターDirectX グラフィックスのカーネルのサブシステムを呼び出すときのアドレス空間、 [ *DxgkDdiQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数。

Miracast セッションを開始すると、モニターが接続されている場合、ディスプレイのミニポート ドライバーを設定する必要があります、Miracast シンク、 [ **DXGK\_子\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_status).**型**メンバーを**StatusMiracast**定数の値も設定する必要があります**DXGK\_子\_状態**.**Miracast**.**接続されている**に**TRUE**、モニター到着 HPD をオペレーティング システムに報告します。 ドライバーを設定する必要があります、 **DXGK\_子\_状態**.**Miracast**.**MiracastMonitorType**シンクに接続されている適切なモニターの種類のメンバー。 このメンバーに設定する必要があります、シンクがモニターの一部である場合は、 **D3DKMDT\_VOT\_MIRACAST**します。

オペレーティング システムを呼び出すと、この EDID を報告する必要があります、ドライバーは、モニターのディスプレイが EDID を知っている場合、 [ *DxgkDdiQueryDeviceDescriptor* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)関数。

ハードウェアの機能、Miracast シンクのモード一覧、およびネットワーク帯域幅、によって、ドライバーは適切なソース モード、ターゲット モード、回転モード、およびスケーリング モードにレポートが必要です。 ターゲット モードでは、ドライバーを正しいに報告する必要があります**VSyncFreqDivider**でメンバー値[ **D3DKMDT\_ビデオ\_信号\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info). オペレーティング システムでは、モニター モードに対して、ターゲット モードと一致して、モニターでサポートされていないすべてのモードの動作を変更します。

 

 






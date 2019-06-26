---
title: ワイヤレス ディスプレイ (Miracast)
description: ワイヤレス (Miracast) の表示は、Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバー必要に応じてサポートできます。 この機能は、新しい Windows 8.1 以降です。
ms.assetid: 1645E14A-EC4A-4EB8-9AFA-6DF0466D2B1A
keywords:
- ワイヤレス ディスプレイ
- Miracast
- Miracast 設計ガイド
- Miracast 参照
- ワイヤレス ディスプレイ Miracast ユーザー モード ドライバーによって呼び出されるコールバック関数
- ワイヤレス ディスプレイ Miracast ユーザー モード ドライバーによって実装される関数
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: df9384f0b556cdbf83b1c48f554e6b2f00e335e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386229"
---
# <a name="wireless-displays-miracast"></a>ワイヤレス ディスプレイ (Miracast)


ワイヤレス (Miracast) の表示は、Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバー必要に応じてサポートできます。 この機能は、新しい Windows 8.1 以降です。

ドライバーと Miracast ディスプレイをサポートするハードウェアの要件の詳細についてを参照してください、 [Windows 10 では、クラス最高の Miracast ソリューションの構築](https://download.microsoft.com/download/3/F/9/3F9F0453-04AE-4E4B-87EF-729FF931C1F9/Building%20best-in-class%20Miracast%20solutions%20with%20Windows%2010%20.docx)ガイドと関連する[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics.WDDM13.DisplayRender.WirelessDisplay**します。

## <a name="span-idmiracastdesignguidespanspan-idmiracastdesignguidespanspan-idmiracastdesignguidespanmiracast-design-guide"></a><span id="Miracast_design_guide"></span><span id="miracast_design_guide"></span><span id="MIRACAST_DESIGN_GUIDE"></span>Miracast 設計ガイド


これらの設計ガイドのセクションでは、ミニポート ドライバーのディスプレイと Miracast ユーザー モード ドライバーが Miracast ディスプレイをサポートする方法について説明します。

-   [Miracast ワイヤレス ディスプレイをサポートする WDDM 表示ミニポート ドライバー タスク](wddm-display-miniport-driver-tasks-to-support-miracast-wireless-displays.md)
-   [Miracast ワイヤレス ディスプレイをサポートする Miracast ユーザー モード ドライバーのタスク](miracast-user-mode-driver-tasks-to-support-miracast-wireless-displays.md)
-   [チャンクと統計情報をエンコード Miracast を報告](reporting-miracast-encode-chunks-and-statistics.md)
-   [Miracast ターゲット DisplayConfig 関数の呼び出し](calling-displayconfig-functions-for-a-miracast-target.md)

## <a name="span-idmiracastreferencespanspan-idmiracastreferencespanspan-idmiracastreferencespanmiracast-reference"></a><span id="Miracast_reference"></span><span id="miracast_reference"></span><span id="MIRACAST_REFERENCE"></span>Miracast 参照


これらの参照セクションには、ドライバーでこの機能を実装する方法について説明します。

### <a name="user-mode-device-driver-interfaces-ddis"></a>ユーザー モード デバイス ドライバー インターフェイス (Ddi)

**ワイヤレス ディスプレイ Miracast ユーザー モード ドライバーによって呼び出されるコールバック関数**

このセクションでは、リファレンスのページには、オペレーティング システムを実装しているワイヤレス ディスプレイ (Miracast) ユーザー モードの機能について説明します。 Miracast ユーザー モード ドライバーだけでは、これらの関数を呼び出すことができます。 

Miracast 表示のコールバック関数へのポインターが返されます、 [MIRACAST_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_callbacks)構造体。

|トピック| 説明 |
|:--|:--|
|[PFN_GET_NEXT_CHUNK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)| 情報を提供 Miracast Microsoft DirectX グラフィックスのカーネルのサブシステムに報告されたチャンクのエンコードは、次のときに、 [DXGK_INTERRUPT_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_interrupt_type)割り込みの種類は DXGK_INTERRUPT_MIRACAST_CHUNK_PROCESSING_COMPLETE します。| 
|[PFN_MIRACAST_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)| カーネル モードのディスプレイのミニポート ドライバーに、同期 I/O 制御要求を送信するユーザー モードのディスプレイ ドライバーによって呼び出されます。|
|[PFN_REGISTER_DATARATE_NOTIFICATIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications)| ネットワーク サービス (QoS) の通知の品質と Miracast 接続の現在のネットワーク帯域幅を受信するオペレーティング システムに登録するユーザー モード ドライバーによって呼び出されます。|
|[PFN_REPORT_SESSION_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)| ユーザー モードのディスプレイ ドライバーによって呼び出される Miracast を現在の状態を報告する接続セッション。|
|[PFN_REPORT_STATISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)| オペレーティング システムを Miracast リンクの統計情報を報告する、ユーザー モードのディスプレイ ドライバーによって呼び出されます。|
 


**ワイヤレス ディスプレイ Miracast ユーザー モード ドライバーによって実装される関数**

このセクションでは、リファレンスのページには、Miracast ユーザー モード ドライバーを実装する必要があるワイヤレス ディスプレイ (Miracast) 関数について説明します。 この種類のドライバーは、スタンドアロンの DLL では実行されます。 

オペレーティング システムへの応答を呼び出し、 [QueryMiracastDriverInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface)関数、Miracast ユーザー モード ドライバーはこれらの関数へのポインターを指定する必要があります、 [MIRACAST_DRIVER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_driver_interface)構造体を除く[pfnDataRateNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification)で宣言されたポインターがある[RegisterForDataRateNotifications](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications)。

|トピック| 説明 |
|:--|:--|
|[PFN_CREATE_MIRACAST_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context)| ユーザー モード Miracast コンテキストを作成するオペレーティング システムによって呼び出されます。|
|[PFN_DESTROY_MIRACAST_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_destroy_miracast_context)| ユーザー モード Miracast コンテキストを破棄するオペレーティング システムによって呼び出されます。|
|[PFN_HANDLE_KMD_MESSAGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_handle_kmd_message)| Miracast ユーザー モード ドライバーがディスプレイのミニポート ドライバーを呼び出すときに受信した非同期のカーネル モードのメッセージを処理するために、オペレーティング システムによって呼び出される、 [DxgkCbMiracastSendMessage](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)関数。|
|[PFN_DATARATE_NOTIFICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification)| Miracast ユーザー モード ドライバー、Miracast ネットワーク リンクのビット レートが変更されたことを通知するオペレーティング システムによって呼び出されます。 この関数がオペレーティング システムに登録されているときに、 **RegisterForDataRateNotifications**関数が呼び出されます。|
|[QUERY_MIRACAST_DRIVER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface)| Miracast ユーザー モードのドライバー インターフェイスを照会するオペレーティング システムによって呼び出されます**MIRACAST_DRIVER_INTERFACE**します。|
|[PFN_START_MIRACAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session)| オペレーティング システムによって呼び出されます、Miracast を開始する接続セッション。|
|[PFN_STOP_MIRACAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)| オペレーティング システムによって呼び出されます、Miracast を開始する接続セッションが開始されて以前への呼び出しによって、 **StartMiracastSession**関数。|
 

**ワイヤレス ディスプレイ (Miracast) 構造および列挙体**

すべてのユーザー モードの構造および Miracast で使用される列挙体は、デバイス ドライバー インターフェイス (Ddi) を表示します。

|トピック |説明 |
|:--|:--|
|[MIRACAST_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_callbacks)| Miracast ユーザー モード ドライバーを呼び出すことができるワイヤレス ディスプレイ (Miracast) ランタイムのコールバック関数へのポインターが含まれています。|
|[MIRACAST_CHUNK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_data)| 含む、ユーザー モード ドライバーは、ワイヤレス ディスプレイ (Miracast) を呼び出すときに使用されるデータをチャンク エンコード[GetNextChunkData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)関数。|
|[MIRACAST_CHUNK_ID](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_id)| ワイヤレス ディスプレイ (Miracast) を識別するストアの情報は、チャンクをエンコードします。|
|[MIRACAST_CHUNK_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)| 指定したワイヤレスに関する情報が含まれています (Miracast) の表示は、チャンクをエンコードします。|
|[MIRACAST_CHUNK_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_chunk_type)| 処理するのには、ワイヤレス ディスプレイ (Miracast) チャンクの情報の種類を指定します。|
|[MIRACAST_DATARATE_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_datarate_stats)| オーディオ/ビデオ エンコーダーのビットレートと失敗したか、再試行の Wi-fi フレームについて、ワイヤレス ディスプレイ (Miracast) pfnDataRateNotify 関数で使用される情報が含まれています。|
|[MIRACAST_DRIVER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_driver_interface)| Miracast ユーザー モード ドライバーによって実装されているワイヤレス ディスプレイ (Miracast) 関数へのポインターが含まれています。|
|[MIRACAST_PROTOCOL_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_protocol_event)| ユーザー モードのディスプレイ ドライバーを報告する必要がありますワイヤレス ディスプレイ (Miracast) プロトコルのイベントの種類を指定します。|
|[MIRACAST_SESSION_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_session_info)| ワイヤレス ディスプレイ (Miracast) に関する情報が接続されているセッションが含まれています。|
|[MIRACAST_STATISTIC_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_statistic_data)| ユーザー モードのディスプレイ ドライバーをオペレーティング システムに報告する Miracast 統計情報データが含まれています。|
|[MIRACAST_STATISTIC_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_statistic_type)| ユーザー モードのディスプレイ ドライバーによって生成される Miracast 統計データの種類を指定します。|
|[MIRACAST_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_status)| ユーザー モードのディスプレイ ドライバーを使用して Miracast 接続の状態を報告する状態の種類を指定します。|
|[MIRACAST_WFD_CONNECTION_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_wfd_connection_stats)| Wi-Fi Direct 接続でのビット レートの情報が含まれています。|

これらの追加のユーザー モードの構造および列挙体 Miracast ディスプレイをサポートし、新規または Windows 8.1 の更新。

-   [**DISPLAYCONFIG\_ターゲット\_ベース\_型**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_base_type) (新規)
-   [**DISPLAYCONFIG\_ビデオ\_信号\_情報**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info) (**AdditionalSignalInfo**子構造の追加)
-   [**DISPLAYCONFIG\_デバイス\_情報\_型**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_device_info_type) (**DISPLAYCONFIG\_デバイス\_情報\_取得\_ターゲット\_基本\_型**定数の追加)
-   [**D3DKMDT\_ビデオ\_信号\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info) (**AdditionalSignalInfo**子構造の追加)
-   [**DISPLAYCONFIG\_デバイス\_情報\_型**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_device_info_type) (**DISPLAYCONFIG\_デバイス\_情報\_取得\_ターゲット\_基本\_型**定数の追加)

### <a name="kernel-mode-ddis"></a>カーネル モード Ddi

**ワイヤレス ディスプレイ (Miracast) 表示コールバック インターフェイス**

Miracast 表示のコールバック インターフェイスには、(Miracast) のワイヤレス ディスプレイをサポートする Microsoft DirectX グラフィックスのカーネル サブシステムによって実装されている関数が含まれています。 このインターフェイスは、以降の Windows 8.1 でサポートされます。

このセクションには、によって Windows 表示 Driver Model (WDDM) 1.3 と呼ばれ、ミニポート ドライバーを後で表示されるこれらのカーネル モード機能のリファレンス ページが含まれています。

|トピック |説明 |
|:--|:--|
|[DXGKCB_MIRACAST_SEND_MESSAGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)|ユーザー モードのディスプレイ ドライバーには、非同期メッセージを送信します。|
|[DXGKCB_MIRACAST_SEND_MESSAGE_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)|メッセージがいるときに、カーネル モードで呼び出されますへの呼び出しでは、ユーザー モード ドライバーに送信される、 **DxgkCbMiracastSendMessage**関数が完了したか、取り消されました。|
|[DXGKCB_MIRACAST_REPORT_CHUNK_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)|レポートについては、エンコードのチャンクにディスプレイのミニポート ドライバーによって呼び出されます。|

これらの関数へのポインターを入力して、ディスプレイのミニポート ドライバー、 [DXGK_MIRACAST_DISPLAY_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_display_callbacks)構造体。

**ワイヤレス ディスプレイ (Miracast) インターフェイス**

このセクションには、カーネル モードの機能 (Miracast) のワイヤレス ディスプレイをサポートする表示ミニポート ドライバーによって実装されているが含まれています。 このインターフェイスは、以降の Windows 8.1 でサポートされます。

Miracast インターフェイスの関数へのポインターが返されます、 [DXGK_MIRACAST_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_interface)構造体。

|トピック |説明 |
|:--|:--|
|[DXGKCB_MIRACAST_SEND_MESSAGE_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)|DxgkCbMiracastSendMessage 関数の呼び出しでは、ユーザー モード ドライバーに送信されたメッセージが完了または取り消されたときに、カーネル モードで呼び出されます。|
|[DXGKDDI_MIRACAST_CREATE_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)|Miracast デバイス用のカーネル モードのコンテキストを作成します。|
|[DXGKDDI_MIRACAST_DESTROY_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)|Miracast device のインスタンスを破棄します。|
|[DXGKDDI_MIRACAST_HANDLE_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)|ディスプレイのミニポート ドライバーが MiracastIoControl 関数にユーザー モードのディスプレイ ドライバー呼び出しに対する応答で、同期 I/O 制御要求を処理することを要求するオペレーティング システムによって呼び出されます。|
|[DXGKDDI_MIRACAST_QUERY_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps) |現在のディスプレイ アダプターの Miracast 機能を照会します。 オペレーティング システムは、ディスプレイ アダプターが最初に起動し、返される機能を格納している場合にのみ、この関数を呼び出します。|


これらの追加のカーネル モードの構造および列挙体 Miracast ディスプレイをサポートし、新規または Windows 8.1 の更新。

-   [**DXGK\_MIRACAST\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_caps)
-   [**D3DKMDT\_ビデオ\_出力\_テクノロジ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology) (**D3DKMDT\_VOT\_MIRACAST**定数の追加)
-   [**D3DKMDT\_ビデオ\_信号\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info) (**AdditionalSignalInfo**子構造の追加)
-   [**DXGK\_子\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_status) (**Miracast**子構造の追加)
-   [**DXGK\_子\_状態\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ne-dispmprt-_dxgk_child_status_type) (**StatusMiracast**定数の追加)
-   [**DXGKARGCB\_通知\_INTERRUPT\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data) (**MiracastEncodeChunkCompleted**子構造の追加)

 

 






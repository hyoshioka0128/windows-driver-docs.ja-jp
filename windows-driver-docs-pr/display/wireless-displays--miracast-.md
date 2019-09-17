---
title: ワイヤレス ディスプレイ (Miracast)
description: ワイヤレス (Miracast) ディスプレイは、必要に応じて、Windows Display Driver Model (WDDM) 1.3 以降のドライバーでサポートされます。 この機能は Windows 8.1 以降の新機能です。
ms.assetid: 1645E14A-EC4A-4EB8-9AFA-6DF0466D2B1A
keywords:
- ワイヤレスディスプレイ
- Miracast
- Miracast デザインガイド
- Miracast リファレンス
- ワイヤレス表示コールバック関数が Miracast ユーザーモードドライバーによって呼び出される
- Miracast ユーザーモードドライバーによって実装されるワイヤレス表示関数
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1d505a80c086e8bc0ccd52d4286bc959ae2f2675
ms.sourcegitcommit: 156768ee079729d04a25b4ae08983f81b1f6d200
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70161347"
---
# <a name="wireless-displays-miracast"></a>ワイヤレス ディスプレイ (Miracast)


ワイヤレス (Miracast) ディスプレイは、必要に応じて、Windows Display Driver Model (WDDM) 1.3 以降のドライバーでサポートされます。 この機能は Windows 8.1 以降の新機能です。

Miracast 表示をサポートするドライバーとハードウェアの要件の詳細については、「 [Windows 10 を使用した最高クラスのワイヤレス投影ソリューションの構築](https://docs.microsoft.com/windows-hardware/design/device-experiences/wireless-projection)」ガイドと、関連する[whck ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)**を参照してください。WDDM13 を WirelessDisplay**しています。

## <a name="span-idmiracast_design_guidespanspan-idmiracast_design_guidespanspan-idmiracast_design_guidespanmiracast-design-guide"></a><span id="Miracast_design_guide"></span><span id="miracast_design_guide"></span><span id="MIRACAST_DESIGN_GUIDE"></span>Miracast デザインガイド


これらの設計ガイドのセクションでは、ディスプレイミニポートドライバーと Miracast ユーザーモードドライバーが Miracast の表示をサポートする方法について説明します。

-   [WDDM Miracast ワイヤレスディスプレイをサポートするミニポートドライバータスクの表示](wddm-display-miniport-driver-tasks-to-support-miracast-wireless-displays.md)
-   [Miracast ワイヤレスディスプレイをサポートする miracast ユーザーモードドライバータスク](miracast-user-mode-driver-tasks-to-support-miracast-wireless-displays.md)
-   [Miracast エンコードチャンクと統計情報のレポート](reporting-miracast-encode-chunks-and-statistics.md)
-   [Miracast ターゲットの DisplayConfig 関数の呼び出し](calling-displayconfig-functions-for-a-miracast-target.md)

## <a name="span-idmiracast_referencespanspan-idmiracast_referencespanspan-idmiracast_referencespanmiracast-reference"></a><span id="Miracast_reference"></span><span id="miracast_reference"></span><span id="MIRACAST_REFERENCE"></span>Miracast リファレンス


以下の参照セクションでは、この機能をドライバーに実装する方法について説明します。

### <a name="user-mode-device-driver-interfaces-ddis"></a>ユーザーモードデバイスドライバーインターフェイス (DDIs)

**ワイヤレス表示コールバック関数が Miracast ユーザーモードドライバーによって呼び出される**

このセクションのリファレンスページでは、オペレーティングシステムによって実装されるワイヤレスディスプレイ (Miracast) のユーザーモード関数について説明します。 これらの関数を呼び出すことができるのは、Miracast ユーザーモードドライバーだけです。 

Miracast 表示コールバック関数へのポインターは、 [MIRACAST_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_callbacks)構造体で返されます。

|トピック| 説明 |
|:--|:--|
|[PFN_GET_NEXT_CHUNK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)| [DXGK_INTERRUPT_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_interrupt_type)割り込みの種類が DXGK_INTERRUPT_MIRACAST_CHUNK_PROCESSING_COMPLETE の場合に Microsoft DirectX graphics カーネルサブシステムに報告された次の Miracast エンコードチャンクに関する情報を提供します。| 
|[PFN_MIRACAST_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)| カーネルモードディスプレイミニポートドライバーに同期 i/o 制御要求を送信するために、ユーザーモードのディスプレイドライバーによって呼び出されます。|
|[PFN_REGISTER_DATARATE_NOTIFICATIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications)| ネットワークのサービス品質 (QoS) 通知および Miracast 接続の現在のネットワーク帯域幅を受信するために、オペレーティングシステムに登録するために、ユーザーモードドライバーによって呼び出されます。|
|[PFN_REPORT_SESSION_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)| 現在の Miracast 接続セッションの状態を報告するために、ユーザーモードの表示ドライバーによって呼び出されます。|
|[PFN_REPORT_STATISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)| オペレーティングシステムへの Miracast リンクの統計を報告するために、ユーザーモードの表示ドライバーによって呼び出されます。|
 


**Miracast ユーザーモードドライバーによって実装されるワイヤレス表示関数**

このセクションのリファレンスページでは、Miracast ユーザーモードドライバーで実装する必要があるワイヤレス表示 (Miracast) 関数について説明します。 この種類のドライバーは、スタンドアロン DLL で実行されます。 

[QueryMiracastDriverInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface)関数へのオペレーティングシステムの呼び出しに応答して、Miracast ユーザーモードドライバーは[MIRACAST_DRIVER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_driver_interface)構造体でこれらの関数へのポインターを提供する必要があります。ただし、[pfnDataRateNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification) は例外で、これは [RegisterForDataRateNotifications](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications) で宣言されたポインターを持ちます。

|トピック| 説明 |
|:--|:--|
|[PFN_CREATE_MIRACAST_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context)| ユーザーモードの Miracast コンテキストを作成するために、オペレーティングシステムによって呼び出されます。|
|[PFN_DESTROY_MIRACAST_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_destroy_miracast_context)| ユーザーモードの Miracast コンテキストを破棄するために、オペレーティングシステムによって呼び出されます。|
|[PFN_HANDLE_KMD_MESSAGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_handle_kmd_message)| ディスプレイミニポートドライバーが[DxgkCbMiracastSendMessage](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)関数を呼び出したときに、Miracast ユーザーモードドライバーによって受信される非同期カーネルモードメッセージを処理するために、オペレーティングシステムによって呼び出されます。|
|[PFN_DATARATE_NOTIFICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification)| Miracast ネットワークリンクのビットレートが変更されたことを Miracast ユーザーモードドライバーに通知するために、オペレーティングシステムによって呼び出されます。 この関数は、 **RegisterForDataRateNotifications**関数が呼び出されたときにオペレーティングシステムに登録されます。|
|[QUERY_MIRACAST_DRIVER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface)| Miracast ユーザーモードドライバーインターフェイス ( **MIRACAST_DRIVER_INTERFACE**) に対してクエリを実行するために、オペレーティングシステムによって呼び出されます。|
|[PFN_START_MIRACAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session)| Miracast 接続セッションを開始するために、オペレーティングシステムによって呼び出されます。|
|[PFN_STOP_MIRACAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)| **StartMiracastSession**関数の呼び出しによって以前に開始された Miracast 接続セッションを開始するために、オペレーティングシステムによって呼び出されます。|
 

**ワイヤレスディスプレイ (Miracast) の構造と列挙体**

Miracast で使用されるすべてのユーザーモード構造体と列挙には、デバイスドライバーインターフェイス (DDIs) が表示されます。

|トピック |説明 |
|:--|:--|
|[MIRACAST_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_callbacks)| Miracast ユーザーモードドライバーが呼び出すことができるワイヤレス表示 (Miracast) ランタイムコールバック関数へのポインターを格納します。|
|[MIRACAST_CHUNK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_data)| ユーザーモードドライバーが wireless display (Miracast) [GetNextChunkData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)関数を呼び出すときに使用されるエンコードチャンクデータを格納します。|
|[MIRACAST_CHUNK_ID](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_id)| ワイヤレス表示 (Miracast) エンコードチャンクを識別する情報を格納します。|
|[MIRACAST_CHUNK_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)| 指定されたワイヤレスディスプレイ (Miracast) のエンコードチャンクに関する情報を格納します。|
|[MIRACAST_CHUNK_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_chunk_type)| 処理するワイヤレス表示 (Miracast) のチャンク情報の種類を指定します。|
|[MIRACAST_DATARATE_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_datarate_stats)| オーディオ/ビデオエンコーダーのビットレートと失敗または再試行された Wi-fi フレームに関するワイヤレスディスプレイ (Miracast) pfnDataRateNotify 関数で使用される情報を格納します。|
|[MIRACAST_DRIVER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_driver_interface)| Miracast ユーザーモードドライバーによって実装されるワイヤレス表示 (Miracast) 関数へのポインターが含まれています。|
|[MIRACAST_PROTOCOL_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_protocol_event)| ユーザーモード表示ドライバーで報告する必要があるワイヤレス表示 (Miracast) プロトコルイベントの種類を指定します。|
|[MIRACAST_SESSION_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_session_info)| ワイヤレスディスプレイ (Miracast) に接続されたセッションに関する情報を格納します。|
|[MIRACAST_STATISTIC_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_statistic_data)| ユーザーモードで表示されるドライバーがオペレーティングシステムに報告する Miracast 統計データを格納します。|
|[MIRACAST_STATISTIC_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_statistic_type)| ユーザーモード表示ドライバーによって生成される Miracast 統計データの種類を指定します。|
|[MIRACAST_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_status)| ユーザーモード表示ドライバーが Miracast 接続状態を報告するために使用するステータスの種類を指定します。|
|[MIRACAST_WFD_CONNECTION_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_wfd_connection_stats)| Wi-fi Direct 接続のビットレート情報が含まれています。|

これらの追加のユーザーモード構造体と列挙型では、Miracast がサポートされており、Windows 8.1 の新しいまたは更新されています。

-   [**Displayconfig\_ターゲット\_基本\_データ型**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_base_type)(新規)
-   [**Displayconfig\_ビデオ\_シグナル情報\_** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info) (**additionalsignalinfo**子構造体が追加されました)
-   [**DISPLAYCONFIG\_デバイス\_情報の\_種類**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_device_info_type) (**DISPLAYCONFIG\_デバイス情報\_GETTARGET 基本型\_)\_\_\_** 定数の追加)
-   [**D3DKMDT\_ビデオシグナル情報\_(additionalsignalinfo 子構造体が追加されました)\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)
-   [**DISPLAYCONFIG\_デバイス\_情報の\_種類**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_device_info_type) (**DISPLAYCONFIG\_デバイス情報\_GETTARGET 基本型\_)\_\_\_** 定数の追加)

### <a name="kernel-mode-ddis"></a>カーネルモード DDIs

**ワイヤレスディスプレイ (Miracast) のコールバックインターフェイスの表示**

Miracast 表示コールバックインターフェイスには、ワイヤレス (Miracast) ディスプレイをサポートするために Microsoft DirectX graphics カーネルサブシステムによって実装される関数が含まれています。 このインターフェイスは Windows 8.1 以降でサポートされています。

このセクションには、Windows Display Driver Model (WDDM) 1.3 以降でミニポートドライバーを表示するカーネルモード関数の参照ページが含まれています。

|トピック |説明 |
|:--|:--|
|[DXGKCB_MIRACAST_SEND_MESSAGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)|ユーザーモードの表示ドライバーに非同期メッセージを送信します。|
|[DXGKCB_MIRACAST_SEND_MESSAGE_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)|**DxgkCbMiracastSendMessage**関数の呼び出しを使用してユーザーモードドライバーに送信されたメッセージが完了したか、取り消されたときに、カーネルモードで呼び出されます。|
|[DXGKCB_MIRACAST_REPORT_CHUNK_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)|エンコードチャンクに関する情報を報告するために、ディスプレイミニポートドライバーによって呼び出されます。|

表示ミニポートドライバーは、 [DXGK_MIRACAST_DISPLAY_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_display_callbacks)構造体のこれらの関数へのポインターを入力する必要があります。

**ワイヤレスディスプレイ (Miracast) インターフェイス**

このセクションには、ワイヤレス (Miracast) ディスプレイをサポートするディスプレイミニポートドライバーによって実装されるカーネルモード関数が含まれています。 このインターフェイスは Windows 8.1 以降でサポートされています。

[DXGK_MIRACAST_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_interface)構造体では、Miracast インターフェイス関数へのポインターが返されます。

|トピック |説明 |
|:--|:--|
|[DXGKCB_MIRACAST_SEND_MESSAGE_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)|DxgkCbMiracastSendMessage 関数の呼び出しを使用してユーザーモードドライバーに送信されたメッセージが完了したか、取り消されたときに、カーネルモードで呼び出されます。|
|[DXGKDDI_MIRACAST_CREATE_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)|Miracast デバイスのカーネルモードコンテキストを作成します。|
|[DXGKDDI_MIRACAST_DESTROY_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)|Miracast デバイスのインスタンスを破棄します。|
|[DXGKDDI_MIRACAST_HANDLE_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)|MiracastIoControl 関数に対するユーザーモードの表示ドライバーの呼び出しに応答して、ディスプレイミニポートドライバーが同期 i/o 制御要求を処理するように要求するために、オペレーティングシステムによって呼び出されます。|
|[DXGKDDI_MIRACAST_QUERY_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps) |現在のディスプレイアダプターの Miracast 機能に対してクエリを行います。 オペレーティングシステムは、ディスプレイアダプターが最初に起動されたときにのみこの関数を呼び出し、返された機能を格納します。|


これらの追加のカーネルモード構造体と列挙型では、Miracast がサポートされており、Windows 8.1 の新しいまたは更新されています。

-   [**DXGK\_MIRACAST\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_caps)
-   [**D3DKMDT\_ビデオ出力テクノロジ\_(D3DKMDT vot MIRACAST 定数の追加)\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology) **\_\_**
-   [**D3DKMDT\_ビデオシグナル情報\_(additionalsignalinfo 子構造体が追加されました)\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)
-   [**DXGK\_子ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_status) (**Miracast**子構造が追加されました)
-   [**DXGK\_子状態の\_種類 (statusmiracast 定数が追加されました)\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ne-dispmprt-_dxgk_child_status_type)
-   [**Dxgkargcb\_通知\_割り込み\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data) (**MiracastEncodeChunkCompleted**子構造が追加されました)

 

 






---
title: ワイヤレス ディスプレイをサポートする Miracast ユーザー モード ドライバー
description: Miracast ワイヤレス表示を有効にするには、スタンドアロン、Miracast ユーザー モード ドライバーを実装する一意の DLL を作成する必要があります。
ms.assetid: FF5D7760-2407-487A-8363-7AC3B6385F6C
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 87c6bbeb864a01c562d02e9020868d1cd7f4b7be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385595"
---
# <a name="span-iddisplaymiracastuser-modedrivertaskstosupportmiracastwirelessdisplaysspanmiracast-user-mode-driver-tasks-to-support-miracast-wireless-displays"></a><span id="display.miracast_user-mode_driver_tasks_to_support_miracast_wireless_displays"></span>Miracast ワイヤレス ディスプレイをサポートする Miracast ユーザー モード ドライバーのタスク


Miracast ワイヤレス表示を有効にするには、スタンドアロン、Miracast ユーザー モード ドライバーを実装する一意の DLL を作成する必要があります。 このドライバーは、専用のセッション 0 プロセスに読み込まれます。 デバイスのソフトウェアの設定として、INF ファイルで、ドライバーの名前を追加**MiracastDriverName**:

``` syntax
[MyDevice_DeviceSettings]
HKR,, MiracastDriverName, %REG_SZ%, Miracast.dll
```

DLL エクスポート機能という名前が存在する必要があります[ *QueryMiracastDriverInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface)オペレーティング システムを呼び出すことができます。 このドライバーのバイナリは、既存のマイクロソフトの Direct3D ユーザー モード ディスプレイ ドライバー DLL を使用しないでください。

Miracast ユーザー モード ドライバーが UMDF0 プロセスに読み込まれていないこのドライバーのバージョンの Windows (WOW) で個別の Windows が必要であるに注意してください。 たとえば、64 ビット プロセッサで、ドライバーの 64 ビット バージョンが使用します。

オペレーティング システムが接続されている Miracast セッションの準備を Miracast ユーザー モード ドライバーが呼び出し[ *CreateMiracastContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context)関数。 この関数が呼び出されたときに、Miracast ユーザー モード ドライバーは、Miracast を開始する必要があるソフトウェア リソースには、セッションが接続されているすべてを割り当てます。 この呼び出しで、オペレーティング システムでは、ドライバーは現在 Miracast コンテキストの有効期間中に呼び出すことができるコールバック関数へのポインターも提供します。 リアルタイム ストリーミング プロトコル (RTSP) リンクが確立されると、オペレーティング システムを呼び出します[ *StartMiracastSession* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session) Miracast を実際に開始するには、セッションを接続します。 この関数の呼び出しに応答して、ドライバーは、Winsock を使用する必要があります[ **getaddrinfo** ](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-getaddrinfo)関数、または Miracast シンクのインターネット プロトコル (IP) アドレスを取得して使用するその他の関連する関数ハイパー テキスト キャッシュ プロトコル (HTCP) リモート デスクトップ プロトコル (RDP) のソケットを作成する標準の Winsock 関数。

Miracast ユーザー モード ドライバーでは、オペレーティング システムが指定した呼び出し Miracast 表示が使用可能になる場合[ **MiracastIoControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)ディスプレイのミニポート ドライバーに、I/O 制御要求を送信する関数値をレポートするモニター到着ホットプラグ検出 (HPD) 認識します。 Miracast ユーザー モード ドライバーの Miracast シンク情報と機能のクエリし、を呼び出すことによって、ディスプレイのミニポート ドライバーの監視の説明など、この情報の一部を報告する必要がありますも**MiracastIoControl**します。

セッションが開始されたら、Miracast 接続後、ドライバーを呼び出す必要があるストリーミング データが準備された後、ネットワークに送信する前に、 [ **ReportStatistic** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)コールバック関数オペレーティング システムに Miracast リンクの統計情報を報告します。

Miracast ユーザー モード ドライバーの呼び出し、オペレーティング システムでは、接続されている Miracast セッションが停止したら、 [ *StopMiracastSession* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)関数。 この関数の呼び出しに応答して、ドライバーは作成され、さらにすべてのデータをストリーミングの削除、すべてのソケットを閉じる必要があります。 ドライバーは、オペレーティング システムを設定している RTSP ソケットを閉じないでください。 これもする必要がありますいないに要求を送信モニター出発地、HPD をレポートするディスプレイのミニポート ドライバー。

オペレーティング システムの呼び出しに応答するために、 [ *DestroyMiracastContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_destroy_miracast_context)関数、Miracast ユーザー モード ドライバーはすべてのソフトウェア リソースに割り当てられていることをリリースする必要があります[*CreateMiracastContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context)します。

ディスプレイのミニポート ドライバーが受信すると、 [ *DxgkDdiCommitVidPn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)オペレーティング システムが指定したドライバーを呼び出す必要があります、接続されている Miracast モニターの電源を切ります要求[ *DxgkCbMiracastSendMessage* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)コールバック関数を Miracast ユーザー モード ドライバーにメッセージを送信します。 Miracast ユーザー モード ドライバーは、低電力状態に Miracast シンクを配置する必要があります。

[ **RegisterForDataRateNotifications** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications) Miracast ユーザー モード ドライバーを 1 回、2 つ目のネットワークの構成を受信するオペレーティング システムに登録するコールバック関数を呼び出すことが必要に応じてことができますサービス (QoS) の通知および Miracast 接続の現在のネットワーク帯域幅。 このネットワークの情報は、オペレーティング システムの呼び出しによって提供される、 [ *pfnDataRateNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification)関数。

Miracast ユーザー モード ドライバーでは、オペレーティング システムによって提供されるこれらのオプションのコールバック関数を呼び出すことができますも。

<span id="GetNextChunkData"></span><span id="getnextchunkdata"></span><span id="GETNEXTCHUNKDATA"></span>[**GetNextChunkData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)  
次のエンコードのチャンクについての情報を提供します。

<span id="ReportSessionStatus"></span><span id="reportsessionstatus"></span><span id="REPORTSESSIONSTATUS"></span>[**ReportSessionStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)  
ドライバーは、現在接続されている Miracast セッションの状態を報告するには、この関数を呼び出します。

 

 






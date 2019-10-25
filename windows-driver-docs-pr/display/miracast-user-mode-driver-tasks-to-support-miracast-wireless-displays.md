---
title: ワイヤレスディスプレイをサポートする Miracast ユーザーモードドライバー
description: Miracast ワイヤレス表示を有効にするには、Miracast ユーザーモードドライバーを実装する、スタンドアロンの一意の DLL を作成する必要があります。
ms.assetid: FF5D7760-2407-487A-8363-7AC3B6385F6C
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 2deca12669f942a4ee1a317f1d00b3bad5861216
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840564"
---
# <a name="span-iddisplaymiracast_user-mode_driver_tasks_to_support_miracast_wireless_displaysspanmiracast-user-mode-driver-tasks-to-support-miracast-wireless-displays"></a><span id="display.miracast_user-mode_driver_tasks_to_support_miracast_wireless_displays"></span>Miracast ワイヤレスディスプレイをサポートする miracast ユーザーモードドライバータスク


Miracast ワイヤレス表示を有効にするには、Miracast ユーザーモードドライバーを実装する、スタンドアロンの一意の DLL を作成する必要があります。 このドライバーは、専用のセッション0プロセスで読み込まれます。 INF ファイルの [デバイスソフトウェア設定] にドライバーの名前を**MiracastDriverName**として追加します。

``` syntax
[MyDevice_DeviceSettings]
HKR,, MiracastDriverName, %REG_SZ%, Miracast.dll
```

DLL には、オペレーティングシステムが呼び出すことができる[*QueryMiracastDriverInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface)という名前のエクスポート関数が必要です。 このドライバーバイナリでは、既存の Microsoft Direct3D ユーザーモード表示ドライバー DLL を使用できません。

Miracast ユーザーモードドライバーは UMDF0 プロセスに読み込まれるため、このドライバーの windows on Windows (WOW) バージョンは別途必要ありません。 たとえば、64ビットプロセッサでは、64ビットバージョンのドライバーが使用されます。

オペレーティングシステムが Miracast 接続セッションを準備する準備ができたら、Miracast ユーザーモードドライバーの[*CreateMiracastContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context)関数を呼び出します。 この関数が呼び出されると、Miracast ユーザーモードドライバーは、Miracast 接続セッションを開始するために必要なすべてのソフトウェアリソースを割り当てます。 この呼び出しでは、オペレーティングシステムは、現在の Miracast コンテキストの有効期間中にドライバーが呼び出すことができるコールバック関数へのポインターも提供します。 その後、リアルタイムストリーミングプロトコル (RTSP) リンクが確立された後、オペレーティングシステムは[*StartMiracastSession*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session)を呼び出して、実際に Miracast 接続セッションを開始します。 この関数呼び出しに応答する場合、ドライバーは Winsock [**getaddrinfo**](https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-getaddrinfo)関数またはその他の関連する機能を使用して、Miracast シンクのインターネットプロトコル (IP) アドレスを取得し、標準の Winsock 関数を使用してハイパーテキストキャッシュを作成する必要があります。Protocol (HTCP) リモートデスクトッププロトコル (RDP) ソケット。

Miracast ディスプレイが使用可能になった場合、Miracast ユーザーモードドライバーは、オペレーティングシステムから提供された[**MiracastIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)関数を呼び出して、モニターに到着したホットプラグ検出 (hpd) を報告するために、ディスプレイミニポートドライバーに i/o 制御要求を送信します。認識価値。 また、Miracast ユーザーモードドライバーでは、Miracast シンクの情報や機能に対してクエリを実行し、 **MiracastIoControl**を呼び出すことによって、モニターの説明など、この情報の一部をミニポートドライバーに報告する必要があります。

Miracast 接続セッションが開始され、ストリーミングデータが準備され、ネットワークに送信される前に、ドライバーは、Miracast リンクの統計情報をレポートするために、 [**reportstatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)コールバック関数を呼び出す必要があります。オペレーティング システム。

オペレーティングシステムは、Miracast に接続されたセッションを停止すると、Miracast ユーザーモードドライバーの[*StopMiracastSession*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)関数を呼び出します。 この関数呼び出しに応答して、ドライバーは、作成されたすべてのソケットを閉じ、すべてのデータストリームを削除する必要があります。 ドライバーは、オペレーティングシステムによって指定された RTSP ソケットを閉じることはできません。 また、モニターの出発点として HPD を報告するように、ディスプレイミニポートドライバーに要求を送信することもできません。

[*DestroyMiracastContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_destroy_miracast_context)関数のオペレーティングシステムの呼び出しに応答する場合、Miracast ユーザーモードドライバーは、 [*CreateMiracastContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context)で割り当てられたすべてのソフトウェアリソースを解放する必要があります。

ディスプレイミニポートドライバーが、接続されている Miracast モニターの電源をオフにする[*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)要求を受信する場合、ドライバーは、オペレーティングシステムが提供する[*DxgkCbMiracastSendMessage*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)コールバック関数を呼び出して、メッセージをMiracast ユーザーモードドライバー。 その後、Miracast ユーザーモードドライバーは、Miracast シンクを低電力状態にする必要があります。

[**RegisterForDataRateNotifications**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications) callback 関数は、必要に応じて、オペレーティングシステムに登録して、2つ目のネットワークのサービス品質 (QoS) 通知と現在のネットワークを受信するように、Miracast ユーザーモードドライバーによって呼び出すことができます。Miracast 接続の帯域幅。 このネットワーク情報は、 [*pfnDataRateNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification)関数のオペレーティングシステム呼び出しによって提供されます。

Miracast ユーザーモードドライバーは、オペレーティングシステムによって提供される次のオプションのコールバック関数を呼び出すこともできます。

<span id="GetNextChunkData"></span><span id="getnextchunkdata"></span><span id="GETNEXTCHUNKDATA"></span>[**GetNextChunkData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)  
次のエンコードチャンクに関する情報を提供します。

<span id="ReportSessionStatus"></span><span id="reportsessionstatus"></span><span id="REPORTSESSIONSTATUS"></span>[**ReportSessionStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)  
ドライバーは、この関数を呼び出して、現在の Miracast 接続セッションの状態を報告します。

 

 






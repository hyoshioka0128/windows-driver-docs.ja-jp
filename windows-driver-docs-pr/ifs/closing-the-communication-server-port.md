---
title: 通信サーバー ポートを閉じる
description: 通信サーバー ポートを閉じる
ms.assetid: 43dfa162-0098-4a9b-9272-9da429cb0108
keywords:
- 通信サーバー ポート WDK ファイル システム ミニフィルター
- WDK、ファイル システム ミニフィルターのポート
- サーバーの通信ポートを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3df85e14b3befa15902921e1f90393cb0367a1c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379004"
---
# <a name="closing-the-communication-server-port"></a>通信サーバー ポートを閉じる


## <span id="ddk_closing_the_communication_server_port_if"></span><span id="DDK_CLOSING_THE_COMMUNICATION_SERVER_PORT_IF"></span>


ミニフィルター ドライバーは以前、呼び出すことによって、カーネル モードの通信サーバー ポートを開いた場合[ **FltCreateCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatecommunicationport)、呼び出すことによって、ポートを閉じる必要があります、 [ **FltCloseCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltclosecommunicationport)します。 システムがミニフィルター ドライバーのアンロード中にハングするを防ぐために[ **FilterUnloadCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンは、呼び出す前にこのポートを閉じる必要があります[ **FltUnregisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltunregisterfilter)します。

その接続の任意のクライアント ポートを後に開いたまま、ユーザー モード アプリケーションが、通信サーバーのポートを開いている接続場合、 [ **FltCloseCommunicationPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltclosecommunicationport)を返します。 ただし、ミニフィルター ドライバーが読み込まれると、フィルター マネージャーは、クライアントのポートを閉じられます。

 

 





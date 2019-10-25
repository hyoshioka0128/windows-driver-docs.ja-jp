---
title: 通信サーバー ポートを閉じる
description: 通信サーバー ポートを閉じる
ms.assetid: 43dfa162-0098-4a9b-9272-9da429cb0108
keywords:
- 通信サーバーポート WDK ファイルシステムミニフィルター
- ポート WDK、ファイルシステムミニフィルター
- 通信サーバーのポートを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 500988fc7b6ea75e4454231b5b3bc6bd2adab225
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841474"
---
# <a name="closing-the-communication-server-port"></a>通信サーバー ポートを閉じる


## <span id="ddk_closing_the_communication_server_port_if"></span><span id="DDK_CLOSING_THE_COMMUNICATION_SERVER_PORT_IF"></span>


ミニフィルタードライバーで[**FltCreateCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatecommunicationport)を呼び出してカーネルモード通信サーバーのポートを既に開いている場合は、 [**FltCloseCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclosecommunicationport)を呼び出してポートを閉じる必要があります。 アンロードプロセス中にシステムがハングするのを防ぐため、ミニフィルタードライバーの[**FilterUnloadCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンは、 [**Fltunregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)を呼び出す前にこのポートを閉じる必要があります。

ユーザーモードアプリケーションが通信サーバーポートへの接続を開いている場合、 [**FltCloseCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclosecommunicationport)がを返すと、その接続のすべてのクライアントポートは開かれたままになります。 ただし、フィルタマネージャは、ミニフィルタドライバがアンロードされたときに、すべてのクライアントポートを閉じます。

 

 





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
ms.openlocfilehash: 6ea9e306dc9c8a1a5c718e50f89da148964917bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575073"
---
# <a name="closing-the-communication-server-port"></a>通信サーバー ポートを閉じる


## <span id="ddk_closing_the_communication_server_port_if"></span><span id="DDK_CLOSING_THE_COMMUNICATION_SERVER_PORT_IF"></span>


ミニフィルター ドライバーは以前、呼び出すことによって、カーネル モードの通信サーバー ポートを開いた場合[ **FltCreateCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff541931)、呼び出すことによって、ポートを閉じる必要があります、 [ **FltCloseCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff541871)します。 システムがミニフィルター ドライバーのアンロード中にハングするを防ぐために[ **FilterUnloadCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551085)ルーチンは、呼び出す前にこのポートを閉じる必要があります[ **FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)します。

その接続の任意のクライアント ポートを後に開いたまま、ユーザー モード アプリケーションが、通信サーバーのポートを開いている接続場合、 [ **FltCloseCommunicationPort** ](https://msdn.microsoft.com/library/windows/hardware/ff541871)を返します。 ただし、ミニフィルター ドライバーが読み込まれると、フィルター マネージャーは、クライアントのポートを閉じられます。

 

 





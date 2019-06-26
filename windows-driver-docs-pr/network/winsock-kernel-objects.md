---
title: Winsock カーネル オブジェクト
description: Winsock カーネル オブジェクト
ms.assetid: 1ce9bd19-9159-4a73-96f6-6e2adac886b9
keywords:
- Winsock カーネル WDK がネットワーク接続、オブジェクト
- ネットワーク、WSK WDK オブジェクト
- WDK Winsock カーネル オブジェクト
- WDK Winsock Kernel のソケット オブジェクト
- クライアント オブジェクト WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3107a14ac01228705aa962427a1978044a70e2b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356960"
---
# <a name="winsock-kernel-objects"></a>Winsock カーネル オブジェクト


Winsock カーネル (WSK)[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)に設計された 2 つの主要なオブジェクトの種類です。*クライアント*と*ソケット*します。

<a href="" id="client-object-------"></a>**クライアント オブジェクト**   
A*クライアント オブジェクト*添付ファイル、または WSK アプリケーションと WSK サブシステム間のバインドを表します。 クライアント オブジェクトで表される、 [ **WSK\_クライアント**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)構造体。 クライアント オブジェクトへのポインターは、WSK サブシステムに添付ファイルの処理中に WSK アプリケーションに返されます。 このポインターは、WSK アプリケーションは、クライアント オブジェクト レベルで動作するすべての WSK 関数に渡します。

<a href="" id="socket-object-------"></a>**ソケット オブジェクト**   
A*ソケット オブジェクト*ネットワーク I/O のために使用するネットワーク ソケットを表します。 によって表されるソケット オブジェクト、 [ **WSK\_ソケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_socket)構造体。 ソケット オブジェクトへのポインターは、アプリケーションが新しいソケットを作成するときに、またはアプリケーションが着信接続を受け入れる場合、WSK アプリケーションに返されます。 このポインターは、WSK アプリケーションは、特定のソケットに固有のすべての WSK 関数に渡します。

 

 






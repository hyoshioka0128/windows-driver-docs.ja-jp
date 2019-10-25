---
title: Winsock カーネル オブジェクト
description: Winsock カーネル オブジェクト
ms.assetid: 1ce9bd19-9159-4a73-96f6-6e2adac886b9
keywords:
- Winsock カーネル WDK ネットワーク、オブジェクト
- WSK WDK ネットワーク、オブジェクト
- オブジェクト WDK Winsock カーネル
- ソケットオブジェクト WDK Winsock カーネル
- クライアントオブジェクト WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f84162c203c904ca83121fe57ba3a66497090d6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844374"
---
# <a name="winsock-kernel-objects"></a>Winsock カーネル オブジェクト


Winsock カーネル (WSK)[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)は、*クライアント*と*ソケット*の2つの主要なオブジェクトの種類を中心に設計されています。

<a href="" id="client-object-------"></a>**クライアントオブジェクト**   
*クライアントオブジェクト*は、wsk アプリケーションと wsk サブシステムの間の添付ファイル (バインド) を表します。 クライアントオブジェクトは、 [**Wsk\_クライアント**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)構造体によって表されます。 WSK サブシステムへのアタッチ処理中に、クライアントオブジェクトへのポインターが WSK アプリケーションに返されます。 WSK アプリケーションは、クライアントオブジェクトレベルで動作するすべての WSK 関数にこのポインターを渡します。

<a href="" id="socket-object-------"></a>**ソケットオブジェクト**   
*Socket オブジェクト*は、ネットワーク i/o に使用できるネットワークソケットを表します。 ソケットオブジェクトは[**Wsk\_socket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_socket)構造体によって表されます。 アプリケーションが新しいソケットを作成するとき、またはアプリケーションが受信接続を受け入れるときに、ソケットオブジェクトへのポインターが WSK アプリケーションに返されます。 WSK アプリケーションは、特定のソケットに固有のすべての WSK 関数にこのポインターを渡します。

 

 






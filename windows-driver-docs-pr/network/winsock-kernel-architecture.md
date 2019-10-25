---
title: Winsock カーネルのアーキテクチャ
description: Winsock カーネルのアーキテクチャ
ms.assetid: 3a43c200-4180-4d1b-8ca6-ee82a84b9194
keywords:
- Winsock カーネル WDK ネットワーク, アーキテクチャ
- WSK WDK ネットワーク, アーキテクチャ
- アーキテクチャ WDK Winsock カーネル
- ネットワークモジュール WDK Winsock カーネル
- サブシステム WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b8d257268638e695775146d2760d1e6f856e61c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845041"
---
# <a name="winsock-kernel-architecture"></a>Winsock カーネルのアーキテクチャ


次の図は、Winsock カーネル (WSK) のアーキテクチャを示しています。

![wsk のアーキテクチャを示す図 ](images/wskarch.png)

WSK アーキテクチャの中核となるのが WSK サブシステムです。 WSK サブシステムは、WSK[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)のプロバイダー側を実装する[ネットワークモジュール](network-module.md)です。 WSK サブシステムでは、さまざまなトランスポートプロトコルのサポートを提供するトランスポートプロバイダーが下部にあります。

WSK サブシステムにアタッチされている WSK アプリケーションです。 WSK アプリケーションは、ネットワーク i/o 操作を実行するために WSK NPI のクライアント側を実装するカーネルモードのソフトウェアモジュールです。 (このコンテキストでは、クライアントサーバーシステムで使用されている用語と "client" を混同しないでください)。 の順に移動します。 WSK サブシステムは WSK クライアント NPI の関数を呼び出して、WSK アプリケーションに非同期イベントを通知できます。

Wsk アプリケーションは wsk[登録関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)のセットを使用して wsk サブシステムを検出し、アタッチします。 アプリケーションでは、これらの関数を使用して WSK サブシステムが使用可能であることを動的に検出し、WSK NPI のプロバイダーとクライアント側の実装を構成するディスパッチテーブルを交換できます。

また、WSK アプリケーションは、[ネットワークモジュールレジストラー (NMR)](network-module-registrar2.md)を使用して wsk サブシステムにアタッチすることもできます。 詳細については、「 [WSK の登録と登録解除に NMR を使用する](using-nmr-for-wsk-registration-and-unregistration.md)」を参照してください。

 

 






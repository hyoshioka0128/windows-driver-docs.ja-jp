---
title: Winsock カーネルのアーキテクチャ
description: Winsock カーネルのアーキテクチャ
ms.assetid: 3a43c200-4180-4d1b-8ca6-ee82a84b9194
keywords:
- Winsock カーネル WDK が、ネットワーク アーキテクチャ
- ネットワーク、WSK WDK アーキテクチャ
- WDK Winsock カーネルのアーキテクチャ
- ネットワーク モジュール WDK Winsock カーネル
- WDK Winsock Kernel サブシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03e8ab5395dfe98185500470bcb5a38a33122ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360241"
---
# <a name="winsock-kernel-architecture"></a>Winsock カーネルのアーキテクチャ


Winsock カーネル (WSK) のアーキテクチャは、次の図に表示されます。

![wsk のアーキテクチャを示す図 ](images/wskarch.png)

WSK の中核には、アーキテクチャは、WSK サブシステムです。 WSK サブシステムは、[ネットワーク モジュール](network-module.md)、WSK のプロバイダーの側を実装する[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)します。 WSK サブシステムは、さまざまなトランスポート プロトコルのサポートを提供するその下端上のトランスポート プロバイダーとインターフェイスします。

WSK にアタッチされているサブシステムは、WSK アプリケーションです。 WSK アプリケーションは、ネットワーク I/O 操作を実行するには、クライアント側の WSK NPI を実装するカーネル モード ソフトウェア モジュールです。 (このコンテキストで「クライアント」する必要がありますと混同しないでクライアント/サーバー システムで使用するための用語)。 . WSK サブシステムは、非同期イベントの WSK アプリケーションに通知する NPI WSK クライアントで、関数を呼び出すことができます。

WSK アプリケーションを検出してのセットを使用して、WSK サブシステムにアタッチ[WSK 登録関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。 アプリケーションは、WSK サブシステムが使用可能な場合に動的に検出するために、プロバイダーと WSK NPI のクライアント側の実装を構成するディスパッチ テーブルを交換して、これらの関数を使用できます。

使用して、WSK アプリケーションを WSK サブシステムをアタッチできますまたは、[ネットワーク モジュール レジストラー (NMR)](network-module-registrar2.md)します。 詳細については、次を参照してください。 [WSK の登録と登録解除を使用して NMR](using-nmr-for-wsk-registration-and-unregistration.md)します。

 

 






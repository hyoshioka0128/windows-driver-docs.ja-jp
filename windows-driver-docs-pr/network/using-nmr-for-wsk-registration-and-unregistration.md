---
title: WSK の登録と登録解除への NMR の使用
description: WSK の登録と登録解除への NMR の使用
ms.assetid: 942fb4e6-ec2e-47ab-9b40-2bd0b7c72ec0
keywords:
- Winsock カーネル WDK ネットワーク、登録します。
- Winsock Kernel アプリケーションの登録
- WSK WDK ネットワーク、登録します。
- Winsock カーネル アプリケーションの登録を解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e2726300dcfa42b2eb8b5359dd8e54415369c21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371779"
---
# <a name="using-nmr-for-wsk-registration-and-unregistration"></a>WSK の登録と登録解除への NMR の使用


[Winsock カーネル アプリケーションを登録する](registering-a-winsock-kernel-application.md)と[Winsock カーネル アプリケーションの登録を解除](unregistering-a-winsock-kernel-application.md)のセクションでは、WSK アプリケーションでにアタッチし、を使用して、WSKサブシステムからデタッチする方法について説明します。[WSK 登録関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。 ただし、WSK にもアタッチできる WSK サブシステムを使用して、[ネットワーク モジュール レジストラー (NMR)](network-module-registrar2.md)します。

として、WSK のクライアントに、NMR に WSK アプリケーションを登録できます[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)によって、次のセクションの手順を使用します。

-   [NMR データ構造体の初期化](initializing-nmr-data-structures.md)
-   [WSK サブシステムへの WSK クライアント](attaching-the-wsk-client-to-the-wsk-subsystem.md)
-   [登録を解除し、アンロード、WSK クライアント](unregistering-and-unloading-the-wsk-client.md)

使用して、 [ **WskRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskregister)と[ **WskDeregister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskderegister)関数は、推奨される方法の登録と WSK を登録解除アプリケーション。 [ネットワーク モジュールのレジストラー](network-module-registrar2.md)は引き続き互換性のために使用できます。

 

 






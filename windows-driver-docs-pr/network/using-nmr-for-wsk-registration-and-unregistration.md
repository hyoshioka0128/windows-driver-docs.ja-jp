---
title: WSK の登録と登録解除への NMR の使用
description: WSK の登録と登録解除への NMR の使用
ms.assetid: 942fb4e6-ec2e-47ab-9b40-2bd0b7c72ec0
keywords:
- Winsock カーネル WDK ネットワーク, 登録
- Winsock カーネルアプリケーションを登録しています
- WSK WDK ネットワーク, 登録
- Winsock カーネルアプリケーションの登録解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8952003d5f6c3a6eed3e155b0d0e19dd742ce45
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842978"
---
# <a name="using-nmr-for-wsk-registration-and-unregistration"></a>WSK の登録と登録解除への NMR の使用


「 [Winsock カーネルアプリケーションを登録](registering-a-winsock-kernel-application.md)する」および「 [winsock カーネルアプリケーション](unregistering-a-winsock-kernel-application.md)の登録を解除する」のセクションでは、wsk[登録関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を使用して wsk アプリケーションを wsk サブシステムにアタッチしてデタッチする方法について説明します。 ただし、WSK は、[ネットワークモジュールレジストラー (NMR)](network-module-registrar2.md)を使用して wsk サブシステムにアタッチすることもできます。

WSK アプリケーションは、次のセクションの手順を使用して、WSK[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)のクライアントとして NMR に登録できます。

-   [NMR データ構造体の初期化](initializing-nmr-data-structures.md)
-   [Wsk クライアントを WSK サブシステムにアタッチする](attaching-the-wsk-client-to-the-wsk-subsystem.md)
-   [WSK クライアントの登録解除とアンロード](unregistering-and-unloading-the-wsk-client.md)

WSK アプリケーションを登録および登録解除するには、 [**Wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)関数と[**wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)関数を使用することをお勧めします。 [ネットワークモジュールレジストラー](network-module-registrar2.md)は、互換性のために引き続き使用できます。

 

 






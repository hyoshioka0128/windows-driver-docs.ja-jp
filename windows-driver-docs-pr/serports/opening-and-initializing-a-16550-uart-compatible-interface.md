---
title: 16550 UART 互換インターフェイスを開いて初期化する
description: 16550 UART 互換インターフェイスを開いて初期化する
ms.assetid: 341cc1cb-bbcf-4514-8f5d-8970e49923c2
keywords:
- シリアル ドライバー WDK、16550 UART と互換性のあるインターフェイス
- ユニバーサル非同期の受信側の送信機 WDK シリアル デバイス
- UART WDK シリアル デバイス
- 16550 UART と互換性のあるインターフェイス WDK シリアル デバイス
- 16550 UART と互換性のあるインターフェイスの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29fc6e93ea5bf6936bc5373701036bc51db0a457
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331119"
---
# <a name="opening-and-initializing-a-16550-uart-compatible-interface"></a>16550 UART 互換インターフェイスを開いて初期化する





シリアルは低レベル デバイス フィルター ドライバーとして使用する場合を開くと、フィルター デバイスの初期化に次の考慮事項が適用されます。

-   シリアルでは、フィルター デバイスで同時に 1 つだけ開くをサポートしています。

-   フィルター デバイスは、開いているときに未定義の状態には。

    クライアントは、使用する前に、既知の状態フィルター デバイスを初期化する必要があります。 ユーザー モードのクライアントが使用できる、 [IOCTL\_シリアル\_設定\_Xxx](https://msdn.microsoft.com/library/windows/hardware/ff547466)要求。 ただし、Win32 準拠アプリケーションが Microsoft Windows SDK の Windows ベースのサービスでサポートされている通信関数を使用する必要がありますに注意してください。 カーネル モード クライアントが使用できるは、IOCTL\_シリアル\_Xxx、 [IOCTL\_シリアル\_内部\_Xxx](https://msdn.microsoft.com/library/windows/hardware/ff547480)要求。

 

 





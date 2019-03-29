---
title: シリアル デバイスを開いて初期化する
description: シリアル デバイスを開いて初期化する
ms.assetid: 08266561-4738-4313-b53b-d60081e875c7
keywords:
- シリアル ドライバー WDK、デバイスを開く
- シリアル ドライバー WDK、デバイスの初期化
- シリアル デバイス WDK を開く
- シリアル デバイス、WDK の初期化
- シリアル デバイスの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ba956fcf9980a655a9da970af1fd0bcdfcfca6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572420"
---
# <a name="opening-and-initializing-a-serial-device"></a>シリアル デバイスを開いて初期化する





シリアルは関数のドライバーとして使用するときに開くと、シリアル デバイスを初期化する次の考慮事項が適用されます。

-   シリアルでは、シリアル デバイスで同時に 1 つだけ開くをサポートしています。

-   開かれたとき、デバイスが未定義の状態です。 クライアントは、デバイスを使用する前に既知の状態のデバイスを初期化する必要があります。 ユーザー モードのクライアントは、Microsoft Windows SDK の Windows ベースのサービスでサポートされている通信関数を使用する必要があります。 カーネル モードのクライアントが使用できる、 [IOCTL\_シリアル\_設定\_Xxx](https://msdn.microsoft.com/library/windows/hardware/ff547466)と[IOCTL\_シリアル\_内部\_Xxx](https://msdn.microsoft.com/library/windows/hardware/ff547480)要求。

-   すべてのクライアントは、必要に応じて、シリアル デバイスを開くし、ポートとは、直後に、デバイスを閉じる必要があります。

-   Serenum には、ポートを列挙するために、rs-232 ポートを開く必要があります。 Rs-232 ポートを開くを無期限に保持しているクライアントでは、Serenum は使用しないでください。

 

 





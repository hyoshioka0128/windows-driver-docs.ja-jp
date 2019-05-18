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
ms.openlocfilehash: 8567cdd6cb0fd5e9487a765be8ba6f8c35b66469
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836349"
---
# <a name="opening-and-initializing-a-serial-device"></a>シリアル デバイスを開いて初期化する

シリアルは関数のドライバーとして使用するときに開くと、シリアル デバイスを初期化する次の考慮事項が適用されます。

- シリアルでは、シリアル デバイスで同時に 1 つだけ開くをサポートしています。

- 開かれたとき、デバイスが未定義の状態です。 クライアントは、デバイスを使用する前に既知の状態のデバイスを初期化する必要があります。 ユーザー モードのクライアントは、Microsoft Windows SDK の Windows ベースのサービスでサポートされている通信関数を使用する必要があります。 カーネル モード クライアントが使用できるは、IOCTL\_シリアル\_設定\_Xxx と IOCTL\_シリアル\_内部\_Xxx 要求。 詳細については、次を参照してください。、 [ntddser.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ntddser/)ヘッダー。

- すべてのクライアントは、必要に応じて、シリアル デバイスを開くし、ポートとは、直後に、デバイスを閉じる必要があります。

- Serenum には、ポートを列挙するために、rs-232 ポートを開く必要があります。 Rs-232 ポートを開くを無期限に保持しているクライアントでは、Serenum は使用しないでください。

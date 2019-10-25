---
title: シリアル デバイスを開いて初期化する
description: シリアル デバイスを開いて初期化する
ms.assetid: 08266561-4738-4313-b53b-d60081e875c7
keywords:
- Serial driver WDK、デバイスを開く
- シリアルドライバー WDK、デバイスの初期化
- シリアルデバイス WDK、開く
- シリアルデバイス WDK、初期化
- シリアルデバイスの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af94445882c9c32d0c9479ce536d3289e0df4f97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842441"
---
# <a name="opening-and-initializing-a-serial-device"></a>シリアル デバイスを開いて初期化する

Serial が関数ドライバーとして使用されている場合、シリアルデバイスを開いたり初期化したりする際には、次の点に注意してください。

- シリアルは、シリアルデバイス上で一度に1つだけ開くことができます。

- デバイスが開いたときに未定義の状態になっています。 クライアントは、デバイスを使用する前に、デバイスを既知の状態に初期化する必要があります。 ユーザーモードのクライアントは、Microsoft Windows SDK で Windows ベースサービスによってサポートされている通信機能を使用する必要があります。 カーネルモードクライアントは、IOCTL\_シリアル\_セット\_Xxx および IOCTL\_シリアル\_内部\_Xxx 要求を使用できます。 詳細については、 [ntddser](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddser/)ヘッダーを参照してください。

- すべてのクライアントは、必要に応じてシリアルデバイスを開き、ポートを使用してデバイスをすぐに閉じる必要があります。

- Serenum.sys は、ポートを列挙するために RS-232 ポートを開く必要があります。 RS-232 ポートを永続的に開いているクライアントは、Serenum.sys を使用しないようにする必要があります。

---
title: 16550 UART 互換インターフェイスを開いて初期化する
description: 16550 UART 互換インターフェイスを開いて初期化する
ms.assetid: 341cc1cb-bbcf-4514-8f5d-8970e49923c2
keywords:
- Serial driver WDK、16550 UART 互換インターフェイス
- ユニバーサル非同期受信側-送信機 WDK シリアルデバイス
- UART WDK シリアルデバイス
- 16550 UART 互換インターフェイス WDK シリアルデバイス
- 16550 UART 互換インターフェイスの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d58e25968b7a3c066eb9f86361dca311066494e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842438"
---
# <a name="opening-and-initializing-a-16550-uart-compatible-interface"></a>16550 UART 互換インターフェイスを開いて初期化する

Serial が下位レベルのデバイスフィルタードライバーとして使用されている場合、フィルターデバイスを開いて初期化する際には次の考慮事項が適用されます。

- シリアルでは、フィルターデバイスで一度に1つのオープンのみがサポートされます。

- フィルターデバイスは、開いているときに未定義の状態になっています。

クライアントは、フィルターデバイスを使用する前に、そのデバイスを既知の状態に初期化する必要があります。 ユーザーモードのクライアントは、\_Xxx 要求に設定された IOCTL\_シリアル\_を使用できます。 ただし、Win32 準拠アプリケーションでは、Microsoft Windows SDK の Windows ベースサービスでサポートされている通信機能を使用する必要があることに注意してください。 カーネルモードクライアントでは、IOCTL\_SERIAL\_Xxx と IOCTL\_シリアル\_内部\_Xxx 要求を使用できます。 詳細については、 [ntddser](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddser/)ヘッダーを参照してください。

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
ms.openlocfilehash: 32eae1924f7f04fad3220ed2f7b03722a9f97628
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862831"
---
# <a name="opening-and-initializing-a-16550-uart-compatible-interface"></a>16550 UART 互換インターフェイスを開いて初期化する

Serial が下位レベルのデバイスフィルタードライバーとして使用されている場合、フィルターデバイスを開いて初期化する際には次の考慮事項が適用されます。

- シリアルでは、フィルターデバイスで一度に1つのオープンのみがサポートされます。

- フィルターデバイスは、開いているときに未定義の状態になっています。

クライアントは、フィルターデバイスを使用する前に、そのデバイスを既知の状態に初期化する必要があります。 ユーザーモードのクライアントは、\_Xxx 要求に設定された IOCTL\_シリアル\_を使用できます。 ただし、Win32 準拠アプリケーションでは、Microsoft Windows SDK の Windows ベースサービスでサポートされている通信機能を使用する必要があることに注意してください。 カーネルモードクライアントでは、IOCTL\_SERIAL\_Xxx と IOCTL\_シリアル\_内部\_Xxx 要求を使用できます。 詳細については、 [ntddser](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/)ヘッダーを参照してください。

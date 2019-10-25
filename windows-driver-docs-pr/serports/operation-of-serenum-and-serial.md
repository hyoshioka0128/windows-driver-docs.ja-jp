---
title: Serenum.sys とシリアルの操作
description: Serenum.sys とシリアルの操作
ms.assetid: d14b6655-c031-42dd-921e-b6a09afde86d
keywords:
- Serial driver WDK、運用
- Serenum.sys ドライバー WDK、運用
- Serial driver WDK
- Serenum.sys ドライバー WDK
- シリアルドライバー WDK
- シリアルデバイス WDK、シリアルドライバー
- シリアルデバイス WDK、Serenum.sys ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58cb5c8b89eae23ddfb3742f7a6b20222bed9403
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837972"
---
# <a name="operation-of-serenum-and-serial"></a>Serenum.sys とシリアルの操作

ここでは、の操作に関する次のトピックについて説明します。

[I/o 要求の serenum.sys フィルター処理](serenum-filtering-of-i-o-requests.md)

[Serenum.sys デバイスの列挙](enumerating-serenum-devices.md)

[レガシ COM ポートの列挙](enumerating-legacy-com-ports.md)

[COM ポートの外部名前付け](external-naming-of-com-ports.md)

[シリアルデバイスを開いて初期化する](opening-and-initializing-a-serial-device.md)

[16550 UART 互換インターフェイスを開いて初期化する](opening-and-initializing-a-16550-uart-compatible-interface.md)

[シリアルデバイス割り込みの共有](sharing-a-serial-device-interrupt.md)

[シリアルデバイスの電源投入](powering-up-a-serial-device.md)

[シリアルデバイスの読み取りと書き込みのタイムアウトの設定](setting-read-and-write-timeouts-for-a-serial-device.md)

[RS-232 ポートのプラグアンドプレイシリアルデバイスの取り外し](removing-a-plug-and-play-serial-device-on-an-rs-232-port.md)

[プラグアンドプレイ RS-232 ポートの取り外し](removing-a-plug-and-play-rs-232-port.md)

[シリアルデバイス制御要求](serial-device-control-requests2.md)

[デバッガーが使用する COM ポートの特定](determining-which-com-port-a-debugger-uses.md)

の動作の詳細については、次のリソースを参照してください。

- [ntddser ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/0)

- [シリアルポートドライバーのリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_serports/)

- \\src\\カーネル\\シリアルおよび \\src\\カーネル\\の Windows Driver Kit (WDK) の serenum.sys ディレクトリのサンプルコード https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serenum

- Microsoft Windows SDK の Windows ベースサービスによってサポートされる通信リソース

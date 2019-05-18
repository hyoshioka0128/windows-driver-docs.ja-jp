---
title: Serenum とシリアルの操作
description: Serenum とシリアルの操作
ms.assetid: d14b6655-c031-42dd-921e-b6a09afde86d
keywords:
- シリアル ドライバー WDK、動作
- Serenum ドライバー WDK、動作
- シリアル ドライバー WDK
- Serenum ドライバー WDK
- シリアル ドライバー WDK
- シリアル デバイス シリアル ドライバー WDK
- シリアル デバイス WDK、Serenum ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64ddc6f95f6950807b5d18eb0b05d07814da8adf
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836345"
---
# <a name="operation-of-serenum-and-serial"></a>Serenum とシリアルの操作

このセクションには、オペレーティング Serenum およびシリアルに関する以下のトピックが含まれています。

[I/O 要求のフィルタ リング Serenum](serenum-filtering-of-i-o-requests.md)

[Serenum デバイスの列挙](enumerating-serenum-devices.md)

[従来の COM ポートを列挙します。](enumerating-legacy-com-ports.md)

[COM ポートの外部の名前を付ける](external-naming-of-com-ports.md)

[開くと、シリアル デバイスの初期化](opening-and-initializing-a-serial-device.md)

[開くと、16550 UART と互換性のあるインターフェイスの初期化](opening-and-initializing-a-16550-uart-compatible-interface.md)

[シリアル デバイスの割り込みを共有](sharing-a-serial-device-interrupt.md)

[シリアル デバイスの電源を入れる](powering-up-a-serial-device.md)

[設定を読み取ってシリアル デバイス用のタイムアウトの作成](setting-read-and-write-timeouts-for-a-serial-device.md)

[Rs-232 ポートでプラグ アンド プレイ シリアル デバイスを削除します。](removing-a-plug-and-play-serial-device-on-an-rs-232-port.md)

[プラグ アンド プレイ rs-232 のポートを削除します。](removing-a-plug-and-play-rs-232-port.md)

[シリアル デバイス制御の要求](serial-device-control-requests2.md)

[デバッガーを使用している COM ポートを決定します。](determining-which-com-port-a-debugger-uses.md)

Serenum およびシリアルの動作の詳細については、次のリソースを参照してください。

- [ntddser header](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/0)

- [シリアル ポート ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_serports/)

- サンプル コード、 \\src\\カーネル\\シリアルと\\src\\カーネル\\serenum ディレクトリ Windows Driver Kit (WDK) で https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serenum

- Microsoft Windows SDK の Windows ベースのサービスでサポートされている通信リソース

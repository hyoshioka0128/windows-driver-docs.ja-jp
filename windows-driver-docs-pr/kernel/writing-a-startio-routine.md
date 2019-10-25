---
title: StartIo ルーチンを記述する
description: StartIo ルーチンを記述する
ms.assetid: b2a380ae-549c-4ca2-9c69-1e20c17ed2e6
keywords:
- StartIo ルーチン, StartIo ルーチンについて
- StartIo ルーチン, 書き込み
- i/o 操作の開始
- WDK カーネルを開始する i/o 操作
- Irp WDK カーネル、キュー
- キューの Irp
- Irp のデキュー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe921472969d1d8bd91b5d5f9e3b7e9c03b77fd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835599"
---
# <a name="writing-a-startio-routine"></a>StartIo ルーチンを記述する





その名前が示すように、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンは、物理デバイスで i/o 操作を開始する役割を担います。

最下位レベルのドライバーは、 *StartIo*ルーチンを提供し、i/o マネージャーを使用してシステムによって提供されるデバイスキューに irp をキューに入れます。 一部の下位レベルのドライバーは、独自の補足的な IRP キューを設定および管理するように設計されていますが、通常は*StartIo*ルーチンも提供します。 補足キューの詳細については、「[デバイスキューの設定と使用](setting-up-and-using-device-queues.md)」および「[デバイスキューの管理](managing-device-queues.md)」を参照してください。

FSDs や PnP 機能やフィルタードライバーなどの上位レベルのドライバーでは、パフォーマンスが阻害される可能性があるため、 *StartIo*ルーチンはほとんどありません。 代わりに、ほとんどのファイルシステムドライバーは、Irp の内部キューをセットアップして維持します。 その他の上位レベルのドライバーには、Irp の内部キューがあるか、またはディスパッチルーチンから下位のドライバーに Irp を渡すだけです。 詳細については[、「ドライバーによって管理される IRP キュー](driver-managed-irp-queues.md) 」を参照してください。

[**Iosetstartioattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes)ルーチンを使用して、ドライバーの*StartIo*処理を変更する属性を設定できます。

このセクションは、次のトピックで構成されています。

[最下位レベルのドライバーの StartIo ルーチン](startio-routines-in-lowest-level-drivers.md)

[上位レベルのドライバーの StartIo ルーチン](startio-routines-in-higher-level-drivers.md)

[StartIo ルーチンの考慮事項](points-to-consider-for-startio-routines.md)

 

 





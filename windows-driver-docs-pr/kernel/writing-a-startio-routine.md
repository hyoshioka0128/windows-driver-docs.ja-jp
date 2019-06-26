---
title: StartIo ルーチンの記述
description: StartIo ルーチンの記述
ms.assetid: b2a380ae-549c-4ca2-9c69-1e20c17ed2e6
keywords:
- StartIo ルーチンについての StartIo ルーチン
- 書き込みの StartIo ルーチン
- I/O 操作の開始
- I/O 操作の開始 WDK のカーネル
- Irp WDK カーネルでは、キュー
- キューの Irp
- Irp をデキューする.
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 480a44b015bd461edfd4e82773b87ecb474df0a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374154"
---
# <a name="writing-a-startio-routine"></a>StartIo ルーチンの記述





その名前からわかるように、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンは、物理デバイスの I/O 操作を開始を担当します。

最下位レベルのほとんどのドライバーを提供、 *StartIo*ルーチンとデバイスのシステム提供のキューにキューの Irp に I/O マネージャーに依存します。 設定して、独自の補足の IRP キューを管理する最下位レベルの一部のドライバーが設計されていますが、通常はも提供もこれらを*StartIo*ルーチン。 (補足的なキューの詳細については、次を参照してください[セットアップ、およびデバイスのキューを使用して](setting-up-and-using-device-queues.md)と[を管理するデバイスのキュー](managing-device-queues.md)。)。

Fsd に対して表示される、PnP 関数とフィルター ドライバーなどのより高度なドライバーがめったにありませんが、 *StartIo*ルーチンのため、パフォーマンスが低下することができます。 代わりに、ほとんどのファイル システム ドライバーは、セットアップし、Irp の内部キューを維持します。 その他の高度なドライバーは Irp の内部キューがあるか、またはそのディスパッチ ルーチンから下位のドライバーに Irp を渡すだけです。 参照してください[Driver-Managed IRP キュー](driver-managed-irp-queues.md)詳細についてはします。

使用することができます、 [ **IoSetStartIoAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes)ルーチンを変更する属性の設定を*StartIo*ドライバーの処理します。

このセクションでは、次のトピックについて説明します。

[最下位レベルのドライバーで StartIo ルーチン](startio-routines-in-lowest-level-drivers.md)

[高度なドライバーの StartIo ルーチン](startio-routines-in-higher-level-drivers.md)

[StartIo ルーチンの考慮すべき点](points-to-consider-for-startio-routines.md)

 

 





---
title: ATA ミニポート ドライバー
description: ATA ミニポート ドライバー
ms.assetid: 4e5cf0e3-72c5-43df-b61e-0039c3666de4
keywords:
- ATA ミニポートドライバー WDK
- 記憶域 ATA ミニポートドライバー WDK
- 記憶域ミニポートドライバー WDK、ATA ミニポートドライバー
- ミニポートドライバー WDK 記憶域、ATA ミニポートドライバー
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 01d2d82deca974ee69985a054537414b8670589c
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252439"
---
# <a name="ata-miniport-drivers"></a>ATA ミニポート ドライバー

> [!NOTE]
> ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。

Ata ミニポートドライバーは、ATA ポートドライバーで動作します。 このページには、ata ポートドライバーが呼び出す ATA ミニポートドライバー内に実装されるルーチンが一覧表示されます。 Ata ミニポートドライバーが呼び出すことができるシステム指定の ATA ポートドライバールーチンの一覧については、「 [Ata ポートドライバーサポートルーチン](ata-port-driver-support-routines.md)」を参照してください。

## <a name="ata-controller-interface-routines"></a>ATA コントローラーのインターフェイスルーチン

すべてのベンダーが提供するミニポートドライバーは、コントローラーインターフェイスを定義する一連のルーチンを実装するために必要です。 これらのルーチンを使用することによって、ミニポートドライバーは、システムによって提供されるコントローラードライバー *pciidex*と通信します。

ベンダーが提供するミニポートドライバーは、コントローラードライバーと通信して、ポートとミニポートドライバーの両方を初期化し、ホストバスアダプター (HBA) を構成するために必要なパラメーターを交換します。 ルーチンがこのセクションで省略可能として明示的に識別されていない場合は、必須です。 省略可能なルーチンを実装しない場合は、 [IDE_CONTROLLER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/ns-irb-_ide_controller_interface)構造体の対応する関数ポインターがミニポートドライバーによって NULL に設定されていることを確認する必要があります。

- DriverEntry
- AtaAdapterControl
- AtaControllerChannelEnabled
- AtaControllerTransferModeSelect

## <a name="ata-channel-interface-routines"></a>ATA チャネルインターフェイスルーチン

ベンダーが提供するミニポートドライバーでは、必要に応じて、チャネルインターフェイスを定義する一連のルーチンを実装できます。 これらのルーチンを使用すると、ミニポートドライバーは、ハードウェアに送信されるすべての要求を処理できます。 ミニポートドライバーは、チャネルインターフェイスを部分的に実装することはできません。 ミニポートドライバーが[**Atachannelinitroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportinitializeex)ルーチンをサポートしている場合は、次のルーチンも実装する必要があります。

- AtaChannelInitRoutine
- IdeHwInitialize
- IdeHwBuildIo
- IdeHwStartIo
- IdeHwInterrupt
- IdeHwReset
- IdeHwControl

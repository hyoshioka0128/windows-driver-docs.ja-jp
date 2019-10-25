---
title: 直接 i/o の使用
description: 直接 i/o の使用
ms.assetid: e40b4657-833f-404c-8472-2e33564129a5
keywords:
- ダイレクト i/o WDK カーネル
- WDK i/o のバッファー、ダイレクト i/o
- データバッファー WDK i/o、ダイレクト i/o
- I/o WDK カーネル、ダイレクト i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd0cdd534837fe343fc3f7fcc711920b5a007a7b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838359"
---
# <a name="using-direct-io"></a>直接 i/o の使用





一度に大量のデータを転送できるデバイスのドライバーでは、転送に直接 i/o を使用する必要があります。 サイズの大きい転送にダイレクト i/o を使用すると、割り込みのオーバーヘッドを減らし、バッファー内の i/o に固有のメモリ割り当てとコピー操作をなくすことによって、ドライバーのパフォーマンスが向上します。

一般に、大容量記憶装置ドライバーは、ダイレクトメモリアクセス (DMA) またはプログラムされた i/o (PIO) を使用する最下位のドライバーや、その上にチェーンされている中間ドライバーを含む、転送要求に対して直接 i/o を要求します。

I/o マネージャーは、i/o 操作で次のように直接 i/o が使用されていると判断します。

-   [**Irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)および[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求の場合は、[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の**Flags**メンバーに直接\_IO を設定します。\_ 詳細については、「[デバイスオブジェクトの初期化](initializing-a-device-object.md)」を参照してください。

-   [**Irp\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)と[**irp\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求の場合、IOCTL コードの値には\_DIRECT または METHOD\_OUT のメソッド\_が含まれますIOCTL 値の*Transfertype*値として直接\_します。 詳細については、「 [I/o 制御コードの定義](defining-i-o-control-codes.md)」を参照してください。

直接 i/o を使用するドライバーでは、バッファー内の i/o を使用して一部の Irp を処理することもあります。 特に、ドライバーが読み取りと書き込みの操作に直接 i/o を使用するかどうかに関係なく、 **IRP\_\_MJ**の一部の i/o 制御コードに対しては、バッファー i/o を使用して、データ転送を必要とする\_要求を制御します。

DMA または PIO が使用されているかどうかによって、直接 i/o 転送の設定は若干異なります。 詳細については、以下を参照してください。

[DMA での直接 i/o の使用](using-direct-i-o-with-dma.md)

[Direct i/o と PIO の使用](using-direct-i-o-with-pio.md)

ドライバーは、DMA および PIO 転送中にキャッシュの一貫性を維持するための手順を実行する必要があります。 詳細については、「[キャッシュの一貫性の維持](maintaining-cache-coherency.md)」を参照してください。

 

 





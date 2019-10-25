---
title: SCSI ミニポート ドライバーの DriverEntry ルーチン
description: SCSI ミニポート ドライバーの DriverEntry ルーチン
ms.assetid: b143bb19-2c9e-4e43-841f-a3c47c7f1a1b
keywords:
- DriverEntry WDK storage
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5eba3fdcc63b2efe61b6a69ce76db741f0461bfe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842681"
---
# <a name="scsi-miniport-drivers-driverentry-routine"></a>SCSI ミニポート ドライバーの DriverEntry ルーチン

**Driverentry**ルーチンは、ほとんどの Microsoft Windows カーネルモードドライバーおよびすべての SCSI ミニポートドライバーの最初のエントリポイントです。 ミニポートドライバーの[**Driverentry**](driverentry-of-scsi-miniport-driver.md)ルーチンは、pvoid 型の2つの入力引数を使用して呼び出され、次の操作を行う必要があります。

1. スタック上の[HW_INITIALIZATION_DATA (SCSI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)構造体をゼロで初期化します。

2. **Hwinitializationdatasize**メンバーを**sizeof**(HW_INITIALIZATION_DATA) に設定します。

3. HW_INITIALIZATION_DATA メンバーのドライバー固有の値と HBA 固有の値を設定します。これには、ミニポートドライバーのエントリポイントが含まれます。 次のエントリポイントを設定する必要があります。

   - [*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))
   - [*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))
   - [*HwScsiStartIo*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))
   - [*HwScsiResetBus*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))

    次のエントリポイントは、ドライバーによって提供されるルーチンに設定するか、 **NULL**に設定する必要があります。

  - [*HwScsiInterrupt*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85)) (ミニポートドライバーがポーリングを排他的に使用する場合は**NULL** )
  - [*HwScsiDmaStarted*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557291(v=vs.85)) (HBA で PIO が使用されているか、バスマスターである場合は**NULL** )
  - [*HwScsiAdapterState*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85)) (ミニポートドライバーが NT ベースのオペレーティングシステムプラットフォームでのみ実行される場合、または x86 専用の Windows プラットフォームでも実行するように設計されている場合に、HBA に BIOS と x86 の両方のドライバーがない場合は**NULL** )
  - [*HwScsiAdapterControl*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85)) (ミニポートドライバーがプラグアンドプレイをサポートしていない場合は**NULL** )

4. レガシミニポートドライバーでは、ドライバーによって決定された、ミニポートドライバーの*HwScsiFindAdapter*ルーチンが使用するコンテキストデータを設定します。

5. **Driverentry**ルーチンに入力されたポインター、入力された HW_INITIALIZATION_DATA のアドレス、コンテキストデータのアドレス (存在する場合) を使用して、 [**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)を呼び出します。

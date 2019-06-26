---
title: SCSI ミニポート ドライバーの DriverEntry ルーチン
description: SCSI ミニポート ドライバーの DriverEntry ルーチン
ms.assetid: b143bb19-2c9e-4e43-841f-a3c47c7f1a1b
keywords:
- DriverEntry WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44deea792e1c57be7eb912ee6e7a83602962f950
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384331"
---
# <a name="scsi-miniport-drivers-driverentry-routine"></a>SCSI ミニポート ドライバーの DriverEntry ルーチン


## <span id="ddk_scsi_miniport_drivers_driverentry_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


A [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ルーチンは、ほとんどの Microsoft Windows NT カーネル モード ドライバーとすべての SCSI ミニポート ドライバーの最初のエントリ ポイント。 ミニポート ドライバーの**DriverEntry**ルーチンは PVOID 型の 2 つの入力引数と呼ばれ、次を行う必要があります。

1.  初期化を[ **HW\_初期化\_データ (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)ゼロでスタック上の構造体。

2.  設定、 **HwInitializationDataSize**メンバー **sizeof**(HW\_初期化\_データ)。

3.  ハードウェア ベースのドライバー固有と HBA 固有の値の設定\_初期化\_ミニポート ドライバーのエントリ ポイントを含む、データ メンバー。 次のエントリ ポイントを設定する必要があります。

    -   [*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))
    -   [*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))
    -   [**HwScsiStartIo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))
    -   [*HwScsiResetBus*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))

    次のエントリ ポイントはドライバーによって提供されるルーチンに設定することができますまたはに設定する必要があります**NULL**:

    -   [**HwScsiInterrupt** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85)) (**NULL**ミニポート ドライバーが排他的にポーリングを使用して)
    -   [**HwScsiDmaStarted** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557291(v=vs.85)) (**NULL** HBA が PIO を使用またはバス マスターかどうか)
    -   [**HwScsiAdapterState** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85)) (**NULL** x86 専用の Windows プラットフォーム上にも設計がかどうかまたは実行しますが、HBA は、どちらも、BIOS ミニポート ドライバーは、NT ベースのオペレーティング システム プラットフォームでのみ実行される場合もx86 リアル モード ドライバー)
    -   [**HwScsiAdapterControl** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85)) (**NULL**ミニポート ドライバーがプラグ アンド プレイをサポートしていないかどうか)

4.  従来のミニポート ドライバー、ドライバーにより決定されたコンテキスト データを設定する、ミニポート ドライバーの*HwScsiFindAdapter*ルーチンが使用されます。

5.  呼び出す[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)への入力が、ポインター、 **DriverEntry**ルーチン、塗りつぶされたハードウェア ベースのアドレス\_の初期化\_データ、およびコンテキスト データ、存在する場合のアドレス。

 

 





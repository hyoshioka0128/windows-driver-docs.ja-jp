---
title: SCSI ミニポート ドライバーの DriverEntry ルーチン
description: SCSI ミニポート ドライバーの DriverEntry ルーチン
ms.assetid: b143bb19-2c9e-4e43-841f-a3c47c7f1a1b
keywords:
- DriverEntry WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c60c3f68a70dffb98e4c6e8fe263a4cd1d3896f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573337"
---
# <a name="scsi-miniport-drivers-driverentry-routine"></a>SCSI ミニポート ドライバーの DriverEntry ルーチン


## <span id="ddk_scsi_miniport_drivers_driverentry_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


A [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)ルーチンは、ほとんどの Microsoft Windows NT カーネル モード ドライバーとすべての SCSI ミニポート ドライバーの最初のエントリ ポイント。 ミニポート ドライバーの**DriverEntry**ルーチンは PVOID 型の 2 つの入力引数と呼ばれ、次を行う必要があります。

1.  初期化を[ **HW\_初期化\_データ (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff557456)ゼロでスタック上の構造体。

2.  設定、 **HwInitializationDataSize**メンバー **sizeof**(HW\_初期化\_データ)。

3.  ハードウェア ベースのドライバー固有と HBA 固有の値の設定\_初期化\_ミニポート ドライバーのエントリ ポイントを含む、データ メンバー。 次のエントリ ポイントを設定する必要があります。

    -   [*HwScsiFindAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff557300)
    -   [*HwScsiInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff557302)
    -   [**HwScsiStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff557323)
    -   [*HwScsiResetBus*](https://msdn.microsoft.com/library/windows/hardware/ff557318)

    次のエントリ ポイントはドライバーによって提供されるルーチンに設定することができますまたはに設定する必要があります**NULL**:

    -   [**HwScsiInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff557312) (**NULL**ミニポート ドライバーが排他的にポーリングを使用して)
    -   [**HwScsiDmaStarted** ](https://msdn.microsoft.com/library/windows/hardware/ff557291) (**NULL** HBA が PIO を使用またはバス マスターかどうか)
    -   [**HwScsiAdapterState** ](https://msdn.microsoft.com/library/windows/hardware/ff557278) (**NULL** x86 専用の Windows プラットフォーム上にも設計がかどうかまたは実行しますが、HBA は、どちらも、BIOS ミニポート ドライバーは、NT ベースのオペレーティング システム プラットフォームでのみ実行される場合もx86 リアル モード ドライバー)
    -   [**HwScsiAdapterControl** ](https://msdn.microsoft.com/library/windows/hardware/ff557274) (**NULL**ミニポート ドライバーがプラグ アンド プレイをサポートしていないかどうか)

4.  従来のミニポート ドライバー、ドライバーにより決定されたコンテキスト データを設定する、ミニポート ドライバーの*HwScsiFindAdapter*ルーチンが使用されます。

5.  呼び出す[ **ScsiPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff564645)への入力が、ポインター、 **DriverEntry**ルーチン、塗りつぶされたハードウェア ベースのアドレス\_の初期化\_データ、およびコンテキスト データ、存在する場合のアドレス。

 

 





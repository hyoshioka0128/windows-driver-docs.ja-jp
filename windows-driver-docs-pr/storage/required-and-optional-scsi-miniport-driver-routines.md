---
title: 必須およびオプションの SCSI ミニポート ドライバー ルーチン
description: 必須およびオプションの SCSI ミニポート ドライバー ルーチン
ms.assetid: 6fd1f7af-e8ba-4679-bd8c-f757b57821b0
keywords:
- SCSI ミニポート ドライバー WDK ストレージの必要なルーチン
- SCSI ミニポート ドライバー WDK ストレージ、省略可能なルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27821b58e3fe97dbf8497b07e3292ca002d3e97a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352792"
---
# <a name="required-and-optional-scsi-miniport-driver-routines"></a>必須およびオプションの SCSI ミニポート ドライバー ルーチン

すべての SCSI ミニポート ドライバーは、少なくとも次のシステム定義のルーチンでが必要です。

- [**DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)ミニポート ドライバーを初期化するには

- [*HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300) HBA(s) のドライバーでサポートされているが、マシンで構成されているか (またはかどうか) を決定するには

- [*HwScsiInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff557302)サポートされている HBA(s) を初期化するには

- [**HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323) hba に関連づけてで着信要求の操作を開始するには

- [*HwScsiResetBus* ](https://msdn.microsoft.com/library/windows/hardware/ff557318)バスを処理するためにリセット要求

SCSI ミニポート ドライバーによって各 HBA とドライバーのデザイナーでは、次のシステム定義のルーチンの一部またはすべてがもあります。

- [**HwScsiInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff557312)ミニポート ドライバー ポーリングによってその HBA のすべての I/O 操作を管理するために、HBA が割り込みを発生しない場合にのみ省略可能であるハンドル HBA が生成した割り込みにします。 ただし、排他的なポーリングを使用してその HBA の I/O のスループットとミニポート ドライバーのパフォーマンスに悪影響があります。 このようなミニポート ドライバーが必要も、 [ *HwScsiTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff557327)ルーチン。

- [**HwScsiDisableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557288)と[ **HwScsiEnableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557295)割り込み駆動の I/O 操作に時間がかかる場合、遅延の I/O に処理を処理するには

- *HwScsiTimer* HBA ドライバー デザイナーによって決定された他の目的または長時間の遅延を必要とする時の操作をします。 ミニポート ドライバーが必要、 *HwScsiTimer*ルーチンがある*HwScsiInterrupt*ルーチンを使用できるように、 *HwScsiTimer*の効率的なポーリングの HBA の日常的な。

- [**HwScsiDmaStarted**](https://msdn.microsoft.com/library/windows/hardware/ff557291)、HBA ポート ドライバーによってシステムの DMA コント ローラーがようプログラムされた後、HBA の転送を設定する、システムの DMA コント ローラーを使用している場合に必要な

- [**HwScsiAdapterState**](https://msdn.microsoft.com/library/windows/hardware/ff557278)は省略可能な場合にのみ、HBA に BIOS がないか、x86 リアル モード ドライバーやは x86 専用の Microsoft Windows システムで実行しません。

- [**HwScsiAdapterControl**](https://msdn.microsoft.com/library/windows/hardware/ff557274)、ミニポート ドライバーがプラグ アンド プレイをサポートしている場合に必要な

前のミニポート ドライバーのルーチンを除く[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff552654)、名前がその機能について説明するように選択します。 除く**DriverEntry**、すべてのミニポート ドライバーの最初のエントリ ポイントに必要な名前である、ミニポート ドライバーのルーチンの名前には、ドライバー開発者が何も指定できます。

次のセクションでは、要件と各ミニポート ドライバー ルーチンの機能について説明します。

[SCSI ミニポート ドライバーでのエラー処理](error-handling-in-scsi-miniport-drivers.md)SCSI ミニポート ドライバーのエラー処理の要件について説明します。

## <a name="see-also"></a>関連項目

[HwScsiWmiExecuteMethod](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)

[HwScsiWmiFunctionControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)

[HwScsiWmiQueryDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)

[HwScsiWmiQueryReginfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)

[HwScsiWmiSetDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock)

[HwScsiWmiSetDataItem](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)
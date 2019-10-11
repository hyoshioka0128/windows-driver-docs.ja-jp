---
title: 必須およびオプションの SCSI ミニポート ドライバー ルーチン
description: 必須およびオプションの SCSI ミニポート ドライバー ルーチン
ms.assetid: 6fd1f7af-e8ba-4679-bd8c-f757b57821b0
keywords:
- SCSI ミニポートドライバー WDK ストレージ、必須ルーチン
- SCSI ミニポートドライバー WDK ストレージ、オプションのルーチン
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 08ef78bdaaf8eb2105873622a4640c6454ddff9b
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72256330"
---
# <a name="required-and-optional-scsi-miniport-driver-routines"></a>必須およびオプションの SCSI ミニポート ドライバー ルーチン

ミニポートドライバーの*HwScsiXxx*ルーチンには、ドライバーライターで任意の名前を付けることができます。 **Driverentry**には、必須の名前を指定します。

すべての SCSI ミニポートドライバーには、少なくとも次のシステム定義ルーチンが必要です。

| 必須ルーチン | 説明 |
| ---------------- | ----------- |
| [**DriverEntry**](driverentry-of-scsi-miniport-driver.md) | ミニポートドライバーを初期化します |
| [*HwScsiFindAdapter*](scsi-miniport-driver-s-hwscsifindadapter-routine.md) | ドライバーでサポートされているホストバスアダプター (Hba) がコンピューターで構成されているかどうかを判断します。 |
| [*HwScsiInitialize*](scsi-miniport-driver-s-hwscsiinitialize-routine.md) | サポートされている HBA を初期化します |
| [*HwScsiStartIo*](scsi-miniport-driver-s-hwscsistartio-routine.md) | 受信した要求に対してミニポートの HBA に対する操作を開始します |
| [*HwScsiResetBus*](scsi-miniport-driver-s-hwscsiresetbus-routine.md) | バスリセット要求を処理します |

各 HBA とドライバーデザイナーによって、SCSI ミニポートドライバーには、次のシステム定義ルーチンの一部またはすべてが含まれます。

|  ルーチン | 説明 |
| -------- | ----------- |
| [*HwScsiInterrupt*](scsi-miniport-driver-s-hwscsiinterrupt-routine.md) | HBA によって生成された割り込みを処理します。これは、hba が割り込みを生成しない場合にのみ省略可能で、ポーリングによって、ミニポートドライバーが HBA 上のすべての i/o 操作を管理します。 ただし、ポーリングを排他的に使用すると、ミニポートドライバーのパフォーマンスとその HBA の i/o スループットに悪影響を及ぼします。 このようなミニポートドライバーにも、 [*HwScsiTimer*](scsi-miniport-driver-s-hwscsitimer-routine.md)ルーチンが必要です。 |
| [*HwScsiDisableInterruptsCallback*](scsi-miniport-driver-s-hwscsidisableinterruptscallback-routine.md)と[ *HwScsiEnableInterruptsCallback*](scsi-miniport-driver-s-hwscsienableinterruptscallback-routine.md) | 割り込みドリブン i/o 操作に長い時間がかかる場合は、遅延 i/o 処理を処理します。 |
| [*HwScsiTimer*](scsi-miniport-driver-s-hwscsitimer-routine.md) | HBA に長い遅延が必要な操作、またはドライバーデザイナによって決定されるその他の目的の場合。 ミニポートドライバーに*HwScsiInterrupt*ルーチンがない場合は、 *HwScsiTimer*ルーチンを使用する必要があります。これにより、 *HwScsiTimer*ルーチンを使用して、その HBA の効率的なポーリングを行うことができます。 |
| [*HwScsiDmaStarted*](scsi-miniport-driver-s-hwscsidmastarted-routine.md) | システム dma コントローラーがポートドライバーによってプログラムされた後に、hba がシステム DMA コントローラーを使用して HBA 転送を設定する場合に必要です。 |
| [*HwScsiAdapterState*](scsi-miniport-driver-s-hwscsiadapterstate-routine.md) | HBA に BIOS または x86 のリアルモードドライバーがない場合、または、x86 専用の Microsoft Windows システムでは実行されない場合は、省略可能です。 |
| [*HwScsiAdapterControl*](scsi-miniport-driver-s-hwscsiadaptercontrol-routine.md) | ミニポートドライバーでプラグアンドプレイがサポートされている場合は必須です。 |
| [HwScsiWmiExecuteMethod](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method) | データブロックに関連付けられたメソッドを実行します。 このルーチンは省略可能です。 |
| [HwScsiWmiFunctionControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control) | イベントの通知を有効または無効にします。また、ミニポートドライバーによって収集の負荷が高いと指定されたデータブロックのデータ収集を有効または無効にします。 任意。 |
| [HwScsiWmiQueryDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock) | 1つのインスタンスまたはデータブロックのすべてのインスタンスを取得します。 必須。 |
| [HwScsiWmiQueryReginfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo) | SCSI ポートドライバーによってミニポートドライバーに代わって登録されるデータおよびイベントブロックに関する情報を取得します。 必須。 |
| [HwScsiWmiSetDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock) | データブロックの1つのインスタンス内のすべてのデータ項目を変更します。 任意。 |
| [HwScsiWmiSetDataItem](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem) | データブロックのインスタンス内の1つのデータ項目を変更します。 任意。 |

上記の各ミニポートドライバールーチン ( [**Driverentry**](driverentry-of-scsi-miniport-driver.md)を除く) には、その機能を説明するための名前が付いています。 すべてのミニポートドライバーの初期エントリポイントに必要な名前である**Driverentry**を除き、ミニポートドライバールーチンの名前は、ドライバーライターが選択するすべてのものになります。

[Scsi ミニポートドライバーでのエラー処理で](error-handling-in-scsi-miniport-drivers.md)は、scsi ミニポートドライバーのエラー処理要件について説明します。

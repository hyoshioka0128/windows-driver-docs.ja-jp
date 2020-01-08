---
title: 記憶域周辺機器への要求の処理
description: 記憶域周辺機器への要求の処理
ms.assetid: 3859588e-fc39-4323-a901-8771874e64d2
keywords:
- ストレージクラスドライバー WDK、周辺機器
- クラスドライバー WDK storage、周辺機器
- 周辺機器 WDK ストレージ
- ストレージ周辺機器 WDK
- 周辺機器 WDK ストレージ, ストレージ周辺機器について
- ストレージ周辺機器 WDK, ストレージ周辺機器について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75be72bcfdaa2debf81970f3b24fec05de5d46c8
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606510"
---
# <a name="handling-requests-to-storage-peripherals"></a>記憶域周辺機器への要求の処理

ストレージポートドライバーが基になるバスで要求を実行する必要があるすべての要求について、クラスドライバーは、SCSI コマンド記述子ブロック (CDB) を含む SCSI 要求ブロック (SRB) を持つ IRP を設定する必要があります。 そのため、ほとんどのストレージクラスドライバーには、SRBs を構築するための内部*Buildrequest*ルーチンが1つ以上あります。 このようなルーチンの詳細については、「[ストレージクラスドライバーの BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md)」を参照してください。

また、ストレージクラスドライバーは、基になるストレージポートドライバーに IRP_MJ_SCSI 要求にも渡します。 このような要求は、[ストレージフィルタードライバー](storage-filter-drivers.md)から発生することがあります。

[**IOCTL_SCSI_PASS_THROUGH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)要求については、「 [SCSI パススルー要求の処理](handling-scsi-pass-through-requests.md)」で説明されているように、クラスドライバーは、ポートドライバーに対して IRP_MJ_DEVICE_CONTROL 要求を[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)で渡す前に、ポートドライバーの i/o スタック位置で IRP_MJ_DEVICE_CONTROL するように**minorfunction**コードを設定します。

各記憶域クラスドライバーは、基になる HBA の機能を超える転送要求 (IRP_MJ_READ および IRP_MJ_WRITE) を分割する役割を担います。 その結果、ほとんどのクラスドライバーは、 [Storage Class Driver の SplitTransferRequest ルーチン](storage-class-driver-s-splittransferrequest-routine.md)で説明されている内部の*splittransferrequest*ルーチンを呼び出すか、または読み取りおよび書き込み要求のディスパッチルーチンで同じ機能を実装します。

ストレージ周辺機器に対する要求の処理の詳細については、次のトピックを参照してください。

[SCSI パススルー要求の処理](handling-scsi-pass-through-requests.md)

[ストレージ周辺機器に対する PnP 要求の処理](handling-pnp-requests-to-storage-peripherals.md)

[ストレージ周辺機器への電力要求の処理](handling-power-requests-to-storage-peripherals.md)

[ストレージ要求をキューに格納する](queuing-storage-requests.md)

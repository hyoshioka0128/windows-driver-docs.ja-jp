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
ms.openlocfilehash: 3c87098ee1648551dc5dcdc792eb0fa5e18e68ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845039"
---
# <a name="handling-requests-to-storage-peripherals"></a>記憶域周辺機器への要求の処理


## <span id="ddk_handling_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


ストレージポートドライバーが基になるバスで要求を実行する必要があるすべての要求について、クラスドライバーは、SCSI コマンド記述子ブロック (CDB) を含む SCSI 要求ブロック (SRB) を持つ IRP を設定する必要があります。 そのため、ほとんどのストレージクラスドライバーには、SRBs を構築するための内部*Buildrequest*ルーチンが1つ以上あります。 このようなルーチンの詳細については、「[ストレージクラスドライバーの BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md)」を参照してください。

また、ストレージクラスドライバーは、基になるストレージポートドライバーに IRP\_MJ\_SCSI 要求を渡します。 このような要求は、[ストレージフィルタードライバー](storage-filter-drivers.md)から発生することがあります。

[**IOCTL\_scsi\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)では、 [scsi パススルー要求の処理](handling-scsi-pass-through-requests.md)に関するページで説明されているように、ポートドライバーの I/o スタック位置で**minorfunction**コードを IRP\_MJ\_デバイス\_制御する必要があります。これは、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して、irp\_MJ\_device\_control 要求をポートドライバーに渡す前に行います。

各ストレージクラスドライバーは、基になる HBA の機能を超える転送要求 (IRP\_MJ\_読み取りおよび IRP\_MJ\_書き込み) を分割する役割を担います。 その結果、ほとんどのクラスドライバーは、 [Storage Class Driver の SplitTransferRequest ルーチン](storage-class-driver-s-splittransferrequest-routine.md)で説明されている内部の*splittransferrequest*ルーチンを呼び出すか、または読み取りおよび書き込み要求のディスパッチルーチンで同じ機能を実装します。

ストレージ周辺機器に対する要求の処理の詳細については、次のトピックを参照してください。

[SCSI パススルー要求の処理](handling-scsi-pass-through-requests.md)

[ストレージ周辺機器に対する PnP 要求の処理](handling-pnp-requests-to-storage-peripherals.md)

[ストレージ周辺機器への電力要求の処理](handling-power-requests-to-storage-peripherals.md)

[ストレージ要求をキューに格納する](queuing-storage-requests.md)

 

 





---
title: 記憶域クラス ドライバーでの PnP 初期化の処理
description: 記憶域クラス ドライバーでの PnP 初期化の処理
ms.assetid: 472e52c8-a214-418b-a82f-fd4a9bcc894e
keywords:
- ストレージクラスドライバー WDK、PnP
- クラスドライバー WDK storage、PnP
- PnP WDK ストレージ
- WDK ストレージのプラグアンドプレイ
- ストレージクラスドライバーの初期化
- ストレージクラスドライバー WDK、初期化
- クラスドライバー WDK storage、初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c031265b857e0178c2862fdc034bb708bdf77011
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837557"
---
# <a name="handling-pnp-initialization-in-a-storage-class-driver"></a>記憶域クラス ドライバーでの PnP 初期化の処理


## <span id="ddk_handling_pnp_initialization_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_INITIALIZATION_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


ストレージクラスドライバーの初期化は、すべての PnP ドライバーの初期化とほぼ同じです。

ストレージクラスドライバーの初期化は、PnP マネージャーがドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出してドライバーを読み込んで初期化するときに開始されます。 次に、PnP マネージャーは、ストレージクラスドライバーの[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出し、ターゲットデバイスを表す物理デバイスオブジェクト (PDO) へのポインターを渡します。

この*AddDevice*ルーチンでは、クラスドライバーは[**IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)を呼び出し、SRB\_\_関数を発行\_デバイスコマンド ( [**SCSI\_REQUEST\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)を参照) をデバイスオブジェクトに発行します。レガシクラスドライバーがデバイスを要求しないようにするために返されます。 クラスドライバーは、この初期化フェーズ中に、他のコマンドをデバイスに送信する必要があります。

クラスドライバーがデバイスを正常に要求した場合は、機能デバイスオブジェクト (FDO) を作成し、入力 PDO で[**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)を呼び出すことによってデバイススタックにアタッチします。 *AddDevice*が返された場合、ドライバーは pnp 開始要求 (IRP\_MJ\_pnp を処理する準備ができている必要があります (irp [ **\_\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))。 PnP マネージャーがドライバースタックの構築を完了した後 (クラスドライバーの上と下にある1つ以上のフィルタードライバーが含まれている可能性があります)、ターゲットデバイスのドライバースタックの最上位のドライバーに対して開始要求を発行します。

クラスドライバーがデバイスを正常に要求できない場合は、デバイススタックへの FDO のアタッチを試行せず、単に*AddDevice*ルーチンから成功の状態を返す必要があります。 このようなドライバーは、デバイスの PnP 開始要求を受信しません。ただし、PnP マネージャーは、同じデバイスまたは別のデバイスに対して*AddDevice*ルーチンを再度呼び出します。

ストレージクラスドライバーの初期化の詳細については、次を参照してください。

[ストレージクラスドライバーの DriverEntry ルーチン](storage-class-driver-s-driverentry-routine.md)

[ストレージクラスドライバーの AddDevice ルーチン](storage-class-driver-s-adddevice-routine.md)

「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」も参照してください。

 

 





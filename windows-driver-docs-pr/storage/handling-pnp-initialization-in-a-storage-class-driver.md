---
title: 記憶域クラス ドライバーでの PnP 初期化の処理
description: 記憶域クラス ドライバーでの PnP 初期化の処理
ms.assetid: 472e52c8-a214-418b-a82f-fd4a9bcc894e
keywords:
- 記憶域クラス ドライバー WDK、PnP
- ドライバー WDK の記憶域クラス PnP
- PnP WDK ストレージ
- プラグ アンド プレイ WDK ストレージ
- 記憶域クラス ドライバーの初期化
- 記憶域クラス ドライバー WDK、初期化しています
- ドライバー WDK の記憶域クラスの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dcc6294eec9bbee80c5b0d7a59dced8c4ef21ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378516"
---
# <a name="handling-pnp-initialization-in-a-storage-class-driver"></a>記憶域クラス ドライバーでの PnP 初期化の処理


## <span id="ddk_handling_pnp_initialization_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_INITIALIZATION_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


ストレージ クラス ドライバーの初期化は、任意の PnP ドライバーの初期化とほぼ同じです。

PnP マネージャーがドライバーを呼び出すときに、記憶域クラス ドライバーの初期化が開始されます[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンを読み込み、ドライバーを初期化します。 記憶域クラス ドライバーの PnP マネージャーし[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)日常的な物理デバイス オブジェクト (PDO) へのポインターを渡すターゲット デバイスを表します。

その*AddDevice*クラス ドライバーのルーチンを呼び出す[ **IoGetAttachedDeviceReference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference) 、SRB の問題と\_関数\_要求\_デバイス コマンド (を参照してください[ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)) デバイス オブジェクトに返される、従来のクラス ドライバーがデバイスを要求するを防ぐためにします。 クラス ドライバーする必要がありますいない他のコマンドを送信、デバイスの初期化には、このフェーズ中に。

その機能のデバイス オブジェクト (FDO) を作成し、呼び出すことによって、デバイス スタックにアタッチしますクラス ドライバーが正常にデバイスを要求する場合[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack) PDO 入力します。 ときに*AddDevice*返します、ドライバーは PnP 開始要求を処理するために準備する必要があります (IRP\_MJ\_で PNP、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))。 PnP マネージャーがドライバー スタック (を 1 つまたは複数のフィルター ドライバーのクラス ドライバーの上下階層化を含む可能性があります) を構築する完了した後、ターゲット デバイスのドライバー スタックの最上位のドライバーを開始要求を発行します。

デバイス スタックに FDO をアタッチする読み取ろうとしないでから成功の状態を返すだけクラス ドライバーでは、デバイスは要求が正常にことはできない場合、その*AddDevice*ルーチン。 PnP マネージャーを呼び出すことができますが、このようなドライバーは、デバイスの PnP 開始要求を受信しなかったが、 *AddDevice*同じまたは別のデバイス用にもう一度ルーチン。

記憶域クラス ドライバーを初期化する方法についての詳細については、次を参照してください。

[記憶域クラス ドライバー DriverEntry ルーチン](storage-class-driver-s-driverentry-routine.md)

[記憶域クラス ドライバー AddDevice ルーチン](storage-class-driver-s-adddevice-routine.md)

参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)します。

 

 





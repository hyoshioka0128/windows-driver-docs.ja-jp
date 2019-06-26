---
title: 記憶域クラス ドライバーの ClaimDevice ルーチン
description: 記憶域クラス ドライバーの ClaimDevice ルーチン
ms.assetid: 175b9be6-34a5-4d20-970c-aa9a6880c242
keywords:
- ClaimDevice
- 記憶域デバイスの要求
- クエリ プロパティは、WDK の記憶域を要求します。
- WDk の記憶域の構成情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec72bdf62e6b2af47e79d227969c2c5ab70614ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368220"
---
# <a name="storage-class-drivers-claimdevice-routine"></a>記憶域クラス ドライバーの ClaimDevice ルーチン


## <span id="ddk_storage_class_drivers_claimdevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_CLAIMDEVICE_ROUTINE_KG"></span>


*ClaimDevice* 、ストレージ デバイスを要求するには、ルーチンが通常から呼び出される、[記憶域クラス ドライバー AddDevice ルーチン](storage-class-driver-s-adddevice-routine.md)します。

ストレージ デバイスを要求するには、クラス ドライバーでは、呼び出すことでデバイス オブジェクトへの参照を取得[ **IoGetAttachedDeviceReference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference) PDO クラス ドライバーに渡されると、 *AddDevice*呼び出すには、いずれかを呼び出します内部*ClaimDevice*ルーチンからその*AddDevice*ルーチンまたは同じ機能のインラインを実装します。 A *ClaimDevice* 、SRB のセットアップ ルーチン、**関数**値 SRB\_関数\_要求\_デバイスと、クラスによって返されるデバイス オブジェクトに送信しますドライバーの呼び出しを**IoGetAttachedDeviceReference**します。

*ClaimDevice*ルーチンの割り当てと IRP [ **IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)、I/O 制御コード IOCTL でポート ドライバーの I/O スタックの場所の設定\_SCSI\_EXECUTE\_で SRB へのポインターと NONE **Parameters.Scsi.Srb**します。 *ClaimDevice*にイベント オブジェクトを設定する必要がありますも**KeInitializeEvent** IRP の完了を待機できるようにします。 次に、使用してドライバーを次の下位に IRP を送信[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

IRP が完了したら、 *ClaimDevice*によって返されるデバイス オブジェクトへの参照を解放する必要があります**IoGetAttachedDeviceReference**します。

A *ClaimDevice*ルーチンは、クラス ドライバーから呼び出されるルーチンとして 2 つの役割を使用できる*RemoveDevice*ルーチンまたは*AddDevice*に成功すると、ドライバー主張して、デバイスがデバイス オブジェクトを作成することはできません。 このような場合、 *ClaimDevice* 、SRB での送信、**関数**SRB 値\_関数\_リリース\_デバイス。

 

 





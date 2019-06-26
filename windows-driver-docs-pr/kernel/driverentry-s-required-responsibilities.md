---
title: DriverEntry の必須の役割
description: DriverEntry の必須の役割
ms.assetid: 6e997875-e7b7-43e2-8398-f0574f3a5816
keywords:
- DriverEntry WDK カーネルでは、必要な責任
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8791b91870821e057743b29319fdee8b09565eee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384951"
---
# <a name="driverentrys-required-responsibilities"></a>DriverEntry の必須の役割





必要な注文の責任を[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンは、次のとおり。

1.  ドライバーの標準的なルーチンのエントリ ポイントを指定します。

    ドライバーは、ドライバー オブジェクトまたはドライバーの拡張機能で、標準的な手順の多くのエントリ ポイントを格納します。 このようなエントリ ポイントには、ドライバーの[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン、ディスパッチ ルーチン、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンと[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチン。 たとえば、ドライバーのエントリ ポイントを設定、 *AddDevice*、 [ *DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、および[ *DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンのステートメントで、次のように (*Xxx*ドライバーの特定のベンダーから提供されたプレフィックスにプレース ホルダーです)。

    ```cpp
        :
    DriverObject->DriverExtension->AddDevice = XxxAddDevice;
    DriverObject->MajorFunction[IRP_MJ_PNP] = XxxDispatchPnp;
    DriverObject->MajorFunction[IRP_MJ_POWER] = XxxDispatchPower;
        :
    ```

    Isr など、追加の標準のルーチンまたは[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)システム サポート ルーチンを呼び出すことによって、ルーチンを指定します。 詳細については、個々 の説明を参照してください。[標準ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)します。

2.  作成/さまざまなドライバー全体オブジェクト、型、またはドライバーを使用してリソースを初期化します。 ドライバーはでは、このようなオブジェクトを設定する必要がありますので、最も標準的なルーチンが、デバイスごとにオブジェクトを使用ことに注意してくださいその*AddDevice*ルーチンまたは受信後に、 [ **IRP\_MN\_ 。開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。

    ドライバーは、デバイス専用のスレッドを持っているか、任意のカーネル定義のディスパッチャー オブジェクトで待機の場合、 **DriverEntry**ルーチンが初期化[カーネルのディスパッチャー オブジェクト](kernel-dispatcher-objects.md)します。 (ドライバーは、オブジェクトを使用する方法、によってでは、このタスクを実行、可能性があります代わりにその*AddDevice*ルーチンまたは受信後、 **IRP\_MN\_開始\_デバイス**要求します)。

3.  メモリ割り当てし、不要になったことを解放します。

4.  NTSTATUS かどうか、ドライバーが正常に読み込まれることができますおよび構成、追加、およびそのデバイスを開始するには、PnP マネージャーから要求を処理を示すを返します。 (を参照してください[DriverEntry 戻り値は](driverentry-return-values.md))。

 

 





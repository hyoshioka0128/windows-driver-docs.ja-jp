---
title: 記憶域クラス ドライバーの AddDevice ルーチン
description: 記憶域クラス ドライバーの AddDevice ルーチン
ms.assetid: ff07ae84-2748-44b4-88c6-e67f1d4c9268
keywords:
- AddDevice ルーチン WDK storage
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca0942a63632116577af7f9d25dd8df0dad16436
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845090"
---
# <a name="storage-class-drivers-adddevice-routine"></a>記憶域クラス ドライバーの AddDevice ルーチン


## <span id="ddk_storage_class_drivers_adddevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_ADDDEVICE_ROUTINE_KG"></span>


PnP マネージャーは、そのドライバーによって制御されるデバイスを検出すると、ストレージクラスドライバーの[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出します。 ストレージクラスドライバーの*AddDevice*ルーチン:

-   「[ストレージクラスドライバーの Claimdevice ルーチン](storage-class-driver-s-claimdevice-routine.md)」で説明されているようにデバイスを要求します。または、ドライバーがデバイスを要求できない場合は、ステータス\_SUCCESS を返します。

-   ドライバーがデバイスを正常に要求した場合、はデバイスオブジェクト (FDO) を作成します。

-   アプリケーションやその他のシステムデバイスで使用できるデバイスインターフェイスを登録します。 クラスドライバーは、PnP 開始要求を受信すると、このようなインターフェイスを有効にします。

-   「 [AddDevice ルーチンの記述](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-an-adddevice-routine)」で説明されているように、開始要求を処理するデバイスオブジェクトを準備します。

-   入力 PDO で[**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)を呼び出すことによって、デバイスオブジェクトをデバイススタックにアタッチします。

-   デバイスが既知の電源状態で起動すると、は[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出します。

-   新しいデバイスオブジェクトの初期化フラグを\_て、DO\_デバイスをクリアします。

ストレージクラスドライバーは、 **Ioattachdevicetodevicestack**から返されたポインターを、新しく要求されたデバイスを表す独自のデバイスオブジェクト (FDO) のデバイス拡張機能に格納します。このポインターは、クラスによる*後続のすべての要求で使用する必要があります。ドライバーは、次の下位のドライバーに送信*します。 また、ドライバーはデバイスの拡張機能に入力 PDO へのポインターを格納しますが、 **Ioattachdevicetodevicestack**が返された後、ドライバーは、このようなポインターを使用する PnP **Io * * * Xxx*ルーチンへの呼び出しでのみ、入力 pdo へのポインターを使用する必要があります。引き.

詳細については、「 [AddDevice ルーチンの記述](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-an-adddevice-routine)」を参照してください。

 

 





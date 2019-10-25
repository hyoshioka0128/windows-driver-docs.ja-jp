---
title: 記憶域クラス ドライバーのデバイス拡張の設定
description: 記憶域クラス ドライバーのデバイス拡張の設定
ms.assetid: 9d050d23-39c0-406e-9f4b-2e95d388f5cf
keywords:
- ストレージクラスドライバー WDK、デバイス拡張機能
- クラスドライバー WDK ストレージ、デバイス拡張
- デバイス拡張機能-WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ee66f69ae2845b7c560aad7ab78e37b5d8149ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842610"
---
# <a name="setting-up-a-storage-class-drivers-device-extension"></a>記憶域クラス ドライバーのデバイス拡張の設定


## <span id="ddk_setting_up_a_storage_class_drivers_device_extension_kg"></span><span id="DDK_SETTING_UP_A_STORAGE_CLASS_DRIVERS_DEVICE_EXTENSION_KG"></span>


ストレージクラスドライバーによって作成された各デバイスオブジェクトの[デバイス拡張機能](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-extensions)では、そのドライバーは、 [**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)に渡される PDO へのポインターなど、デバイスの i/o 要求を管理するために使用するドライバーによって決定されたデータを格納します。[**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)によって返されるデバイスオブジェクトへのポインター、独自のデバイスオブジェクトへのバックポインターなど。

ほとんどのストレージクラスドライバーでは、次の情報を格納するためのストレージも提供されます。

-   デバイスの種類に固有のタイムアウト値

    クラスドライバーは、ポートドライバーに送信する SRBs のタイムアウト値を渡すことができます。 SRB\_関数は、各クラスドライバーに代わって\_SCSI 要求 ( [**scsi\_REQUEST\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)) を実行\_ます。 ポートドライバーは、その Srbstatus メンバーが基になるドライバーに要求を送信してから、要求が完了するまでの間隔が指定されたタイムアウトを超えた場合に、その**Srbstatus**メンバーが SRB\_STATUS\_TIMEOUT に設定された SRB を返します。数値.

-   クラスドライバーのエラー処理ルーチンへのポインター

    ストレージクラスドライバーでのエラー処理の詳細については、「[ストレージクラスドライバーの IoCompletion ルーチン](storage-class-driver-s-iocompletion-routines.md)」を参照してください。

-   ドライバーがデバイスでバスプロトコルエラーを保持する回数

-   Sense データ用のドライバーで割り当てられたバッファーへのポインター

    クラスドライバーは、キャッシュに配置された、非ページプールから返される sense データにメモリを割り当てる必要があります。 ドライバーバッファーにメモリを割り当てる方法の詳細については、「[システム領域メモリの割り当て](https://docs.microsoft.com/windows-hardware/drivers/kernel/allocating-system-space-memory)」を参照してください。

-   ドライバーによって決定された**Srbflags**の既定値。クラスドライバーは SRBs で設定します。

-   ドライバーが割り当てた SRBs のルックアサイドリストを設定する場合は、ルックアサイドリストヘッダーへのポインター

    詳細については、「[ルックアサイドリストの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-lookaside-lists)」を参照してください。

-   ページング操作とエラー回復操作 ([ストレージクラスドライバーの ReleaseQueue ルーチン](storage-class-driver-s-releasequeue-routine.md)によって実行される処理など) のために、メモリ不足状態でも成功する必要がある要求に対して、IRP と SRB へのポインターが割り当てられ、予約されます。

-   ポートドライバーによって HBA から収集された[**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)および[**ストレージ\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)へのポインター

    クラスドライバーがこのデータを取得して使用する方法の詳細については、「[ストレージクラスドライバーの GetDescriptor ルーチン](storage-class-driver-s-getdescriptor-routine.md)」を参照してください。

-   デバイス上の状態間の遷移を管理するための、以前の PnP 状態と現在の PnP 状態を示すフラグ

-   冗長な電源要求の処理に余分な作業を行わないように、現在のデバイスの電源状態を示すフラグ

-   ドライバーによって受信されたページング通知要求に基づいて、デバイス上に存在するシステムページングファイルの数 (IRP\_MJ\_PNP と[**irp\_\_、デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification))

ストレージクラスドライバーは、 [**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)によって返されたデバイスオブジェクトポインターを使用せずに、ドライバーの*AddDevice*によってデバイス拡張機能に格納されているデバイスオブジェクトポインターを使用しないで、ストレージポートドライバーを介してデバイスに要求を送信することはできません。ルーチン.

 

 





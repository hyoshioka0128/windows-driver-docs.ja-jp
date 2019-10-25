---
title: ファンクション ドライバーまたはフィルター ドライバー内の AddDevice ルーチン
description: ファンクション ドライバーまたはフィルター ドライバー内の AddDevice ルーチン
ms.assetid: 0a095c17-2295-46df-9908-f306f7fe9f67
keywords:
- 関数ドライバー WDK カーネル
- フィルタードライバーの WDK カーネル
- AddDevice ルーチン WDK カーネル、関数ドライバー
- AddDevice ルーチン WDK カーネル, フィルタードライバー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c93c731e858af297dd601a5102d75b40aa98004e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837277"
---
# <a name="adddevice-routines-in-function-or-filter-drivers"></a>ファンクション ドライバーまたはフィルター ドライバー内の AddDevice ルーチン





関数またはフィルタードライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンでは、次の手順を実行する必要があります。

1.  [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出して、追加するデバイスの機能デバイスオブジェクト (FDO またはフィルター DO) を作成します。

    デバイスオブジェクトの*DeviceName*を指定しないでください。これにより、PnP マネージャーのセキュリティがバイパスされます。 ユーザーモードコンポーネントがデバイスへのシンボリックリンクを必要とする場合は、デバイスインターフェイスを登録します (次の手順を参照してください)。 カーネルモードのコンポーネントにレガシデバイス名が必要な場合、ドライバーはデバイスオブジェクトに名前を付ける必要がありますが、名前付けは推奨されません。

    *DeviceCharacteristics*パラメーターで OPEN\_OPEN FILE\_DEVICE\_を含めます。 この特性によって、i/o マネージャーは、開いているすべての要求について、デバイスオブジェクトに対してセキュリティチェックを実行するように指示します。これには、相対オープンと末尾のファイル名が含まれます。

2.  \[オプション\] デバイスへの1つまたは複数のシンボリックリンクを作成します。

    [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出して、デバイスの機能を登録し、アプリケーションまたはシステムコンポーネントがデバイスを開くために使用できるシンボリックリンクを作成します。 ドライバーは、 [ **\_デバイス要求の開始\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を処理するときに[**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を呼び出すことによって、インターフェイスを有効にする必要があります。 詳細については、「[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)」を参照してください。

3.  デバイス拡張機能にデバイスの PDO へのポインターを格納します。

    PnP マネージャーは、 *AddDevice*への*PhysicalDeviceObject*パラメーターとして PDO へのポインターを提供します。 ドライバーは、 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)などのルーチンの呼び出しで PDO ポインターを使用します。

4.  デバイスの一時状態を追跡するためのデバイス拡張機能のフラグを定義します。たとえば、デバイスの一時停止、削除、および削除を行います。

    たとえば、デバイスが一時停止状態のときに受信 Irp を保持することを示すフラグを1つ定義します。 Irp のキューを作成します (ドライバーがまだ Irp をキューに格納していない場合)。 詳細については[、「irp をキュー](queuing-and-dequeuing-irps.md)に追加する」を参照してください。

    また、 **IO\_** 割り当てて、デバイス拡張機能で\_ロック構造を削除し、この構造体を初期化するために[**Ioinitializer Eremovelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock)を呼び出します。 詳細については、「 [Remove Locks の使用](using-remove-locks.md)」を参照してください。

5.  デバイススタックに送信される i/o 要求に対して i/o マネージャーが使用するバッファリングの種類を指定するには、\_バッファー\_IO また\_はデバイスオブジェクトのダイレクト\_IO フラグビットを設定します。 上位レベルのドライバー、またはスタック内の次に小さいドライバーと同じ値を持つこのメンバー (最上位レベルのドライバーの場合を除く)。 詳細については、「[デバイスオブジェクトの初期化](initializing-a-device-object.md)」を参照してください。

6.  必要に応じて、電源管理の DO\_POWER\_突入電流フラグまた\_は電源\_PAGABLE フラグを設定します。 ページング可能なドライバーは、DO\_POWER\_PAGABLE フラグを設定する必要があります。 デバイスオブジェクトフラグは、通常、デバイスの PDO を作成するときにバスドライバーによって設定されます。 ただし、上位レベルのドライバーでは、FDO またはフィルターを作成するときに、 *AddDevice*ルーチン内のこれらのフラグの値を変更することが必要になる場合があります。 詳細については、「[電源管理用のデバイスオブジェクトフラグの設定](setting-device-object-flags-for-power-management.md)」を参照してください。

7.  ドライバーがこのデバイスを管理するために使用する他のソフトウェアリソース (イベント、スピンロック、その他のオブジェクトなど) を作成または初期化します。 (I/o ポートなどのハードウェアリソースは、IRP\_に応答して、 [ **\_デバイス要求を開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)に応答して、後で構成されます)。

    *AddDevice*ルーチンは、IRQL = パッシブ\_レベルのシステムスレッドコンテキストで実行されるため、初期化時にのみ使用するために[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)で割り当てられたメモリは、ドライバーがページプールを使用しない限り、システムページファイルを保持するデバイスを制御します。 *AddDevice*が制御を返す前に、このようなメモリ割り当てを[**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)と共に解放する必要があります。

8.  デバイスオブジェクトをデバイススタックにアタッチします ([**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack))。

    *ほか*パラメーターで、デバイスの PDO へのポインターを指定します。

    **Ioattachdevicetodevicestack**によって返されるポインターを格納します。 このポインターは、デバイスの次に低いドライバーのデバイスオブジェクトを指します。 Irp をデバイススタックに渡すときに、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)と[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)に対して必須のパラメーターです。

9.  FDO または filter で次のようなステートメントを使用して、DO\_デバイス\_初期化フラグをクリアします。

    ```cpp
    FunctionalDeviceObject->Flags &= ~DO_DEVICE_INITIALIZING;
    ```

10. デバイスの PnP Irp を処理できるように準備します (たとえば、 [**irp\_\_クエリ\_リソース\_の要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)や**IRP\_\_デバイスの開始**)。

ドライバーは、IRP マネージャーによってデバイスに割り当てられたハードウェアリソースの一覧を含む **\_デバイス\_開始**するように、IRP\_を受け取るまでデバイスの制御を開始することはできません。

 

 





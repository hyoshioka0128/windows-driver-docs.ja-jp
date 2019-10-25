---
title: 開始シーケンス
description: 開始シーケンス
ms.assetid: bf88b9de-f4c4-4f9c-9355-603789b9ad3d
keywords:
- アダプタードライバー WDK オーディオ、スタートアップシーケンス
- スタートアップシーケンス WDK オーディオ
- オーディオアダプター WDK、スタートアップシーケンス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb1c2b8cfd1b661b475b3a198a4d7da1ac22b2fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830122"
---
# <a name="startup-sequence"></a>開始シーケンス


## <span id="startup_sequence"></span><span id="STARTUP_SEQUENCE"></span>


アダプタードライバーはカーネルモードドライバーサービスとしてインストールされるため、オペレーティングシステムはシステム起動時にアダプタードライバーを読み込み、ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出します。 **Driverentry**ルーチンは、ドライバーオブジェクトとレジストリパス名という2つのパラメーターを受け取ります。 **Driverentry**は、PortCls 関数[**pcinitializeadapterdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)を、ドライバーオブジェクトとレジストリパス名パラメーターに加え、3番目のパラメーター (アダプタードライバーの[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)関数へのポインター) で呼び出す必要があります。

次の例では、ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数は、 [**pcinitializeadapterdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)ルーチンの3番目のパラメーターとして、ドライバーの[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)関数を指す関数ポインター `MyAddDevice`を渡します。

```cpp
NTSTATUS 
  DriverEntry( 
    PDRIVER_OBJECT  DriverObject,
    PUNICODE_STRING  RegistryPath
    )
  {
      return PcInitializeAdapterDriver(DriverObject, RegistryPath, MyAddDevice);
  }
```

[**Pcinitializeadapterdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)ルーチンは、指定された[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンをドライバーオブジェクトのドライバー拡張機能にインストールし、PortCls ドライバーの IRP ハンドラーをドライバーオブジェクト自体にインストールします。

次のコードは、ドライバーの `MyAddDevice` 関数の実装例です。

```cpp
#define MAX_MINIPORTS 6    // maximum number of miniports
NTSTATUS
  MyAddDevice(
    PDRIVER_OBJECT  DriverObject,
    PDEVICE_OBJECT  PhysicalDeviceObject 
    )
  {
      return PcAddAdapterDevice(DriverObject, PhysicalDeviceObject, MyStartDevice,
                                MAX_MINIPORTS, 0);
  }
```

この関数は、PortCls 関数**Pcaddadapterdevice**を呼び出し、システムによって提供される*物理デバイスオブジェクト (PDO)* に関連付けます。 新しい FDO は、PortCls がデバイスに関するコンテキスト情報を格納するために使用する拡張機能を使用して作成されます。 このコンテキストには、`MyAddDevice`によって提供される `MyStartDevice` 関数ポインターが含まれています。

オペレーティングシステムは、デバイスに割り当てるリソース (割り込み、DMA チャネル、i/o ポートアドレスなど) を決定した後、デバイスに開始要求を送信します (IRP\_は、[ **\_デバイスを起動\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)ます)。 この要求に応答して、PortCls ドライバーの要求ハンドラーは、アダプタードライバーの `MyStartDevice` 関数を呼び出します。これについては、次のコード例を参照してください。

```cpp
NTSTATUS
  MyStartDevice(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp,
    PRESOURCELIST ResourceList
    )
  {
    ...
  }
```

要求ハンドラーは、デバイスオブジェクトへのポインター、IRP\_、\_開始\_デバイスの要求、およびリソースリストを `MyStartDevice` を提供します (「 [Iresourcelist](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)」を参照してください)。 `MyStartDevice` 関数は、開始する必要がある各ミニポートドライバーに必要なリソースにリソースリストを分割します。 次に、この関数は各ミニポートドライバーを起動し、制御を PortCls に返します。これは IRP を完了し、オペレーティングシステムに制御を戻します。

ドライバーのスタートアップコードのその他の例については、Microsoft Windows Driver Kit (WDK) のオーディオアダプタードライバーのサンプルを参照してください。

 

 





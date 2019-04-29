---
title: 開始シーケンス
description: 開始シーケンス
ms.assetid: bf88b9de-f4c4-4f9c-9355-603789b9ad3d
keywords:
- アダプターのドライバー WDK オーディオ、スタートアップ シーケンス
- スタートアップ シーケンス WDK オーディオ
- オーディオ アダプター WDK、スタートアップ シーケンス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f455e1346e47ac97071caa2d9bdafa2bc76f84ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328609"
---
# <a name="startup-sequence"></a>開始シーケンス


## <span id="startup_sequence"></span><span id="STARTUP_SEQUENCE"></span>


カーネル モード ドライバーのサービスとしてインストールされるため、アダプターのドライバー、オペレーティング システムがシステム起動時に、アダプターのドライバーを読み込み、ドライバーの呼び出し[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。 **DriverEntry**ルーチンは 2 つのパラメーターを受け取ります。 ドライバー オブジェクトおよびレジストリのパス名。 **DriverEntry** PortCls 関数を呼び出す必要があります[ **PcInitializeAdapterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff537703)へのポインターであるドライバー オブジェクトとレジストリ パス名のパラメーター、および 3 番目のパラメーターを使用しますアダプタのドライバの[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)関数。

次の例で、ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数が関数ポインターを渡します`MyAddDevice`、ドライバーの指す[ **AddDevice**](https://msdn.microsoft.com/library/windows/hardware/ff540521)関数、3 番目のパラメーターとして、 [ **PcInitializeAdapterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff537703)ルーチン。

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

[ **PcInitializeAdapterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff537703)ルーチンを指定されたインストール[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ドライバー オブジェクトのドライバーの拡張機能の日常的なドライバーで PortCls ドライバーの IRP ハンドラー オブジェクト自体がインストールされます。

次のコードは、ドライバーの実装例`MyAddDevice`関数。

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

この関数は PortCls 関数を呼び出して**PcAddAdapterDevice**に関連付けますと、*物理デバイス オブジェクト (PDO)* システムによって提供されます。 新しい FDO PortCls を使用して、デバイスに関するコンテキスト情報を格納する拡張機能が作成されます。 このコンテキストが含まれています、`MyStartDevice`によって提供される関数ポインター`MyAddDevice`します。

要求を開始するデバイスを送信後、オペレーティング システムが (割り込み、DMA チャネル、I/O ポートのアドレス、およびなど) をデバイスに割り当てるには、どのようなリソースを決定します ([**IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749))。 この要求に応答してで PortCls ドライバーでの要求ハンドラーを呼び出しますアダプター ドライバーの`MyStartDevice`関数で、次のコード例に示します。

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

要求ハンドラーが`MyStartDevice`IRP のデバイス オブジェクトへのポインターで\_MN\_開始\_デバイス要求、およびリソースの一覧 (を参照してください[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976))。 `MyStartDevice`関数は、各ミニポート ドライバーを開始する必要があるに必要なリソースにリソースの一覧をパーティション分割します。 関数は、各ミニポート ドライバーを開始し、IRP が完了して、オペレーティング システムに制御が戻ります PortCls にコントロールを返します。

ドライバーのスタートアップ コードの例については、Microsoft Windows Driver Kit (WDK) でのサンプル オーディオ アダプター ドライバーを参照してください。

 

 





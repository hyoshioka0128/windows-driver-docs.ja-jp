---
title: ドライバー オブジェクト内のドライバー エントリ ポイント
description: ドライバー オブジェクト内のドライバー エントリ ポイント
ms.assetid: f004c2b3-8435-4c25-82e9-aff3911dc316
keywords:
- ドライバーオブジェクト WDK カーネル
- 標準ドライバールーチン WDK カーネル、ドライバーオブジェクト
- ドライバールーチン WDK カーネル、ドライバーオブジェクト
- ルーチン WDK カーネル、ドライバーオブジェクト
- オブジェクト WDK ドライバーオブジェクト
- エントリポイント WDK カーネル
- ドライバーエントリポイント WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67b5f2f3ebc0f5a8ee9deaff9056f320b1ad4525
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836809"
---
# <a name="driver-entry-points-in-driver-objects"></a>ドライバー オブジェクト内のドライバー エントリ ポイント





カーネルモードドライバーでは、次のエントリポイントを driver オブジェクトに指定する必要があります。

-   少なくとも1つのディスパッチルーチンのエントリポイント。これは、PnP、電力、および i/o 操作を要求する Irp を取得するためのものです。

-   **Driverobject-&gt; Driverobject-&gt; AddDevice**の[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンのエントリポイント。

-   Irp の独自のキューを管理している場合の[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンのエントリポイント。

-   ドライバーを動的に読み込んだり、置き換えることができる場合は、ドライバーが割り当てたシステムオブジェクトやメモリなどのシステムリソースを解放するために、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)エントリポイント。 (キーボードドライバーなど、システムの実行中に置き換えることができないドライバーは、*アンロード*ルーチンを提供する必要はありません)。

これらの要件は、対応するクラスまたはポートドライバーがドライバーオブジェクトのエントリポイントを定義するミニポートドライバーには適用されません。 詳細については、デバイスタイプ固有のドキュメントを参照してください。

I/o マネージャーは、ドライバーによって作成されたデバイスオブジェクトに関する情報を、対応するドライバーオブジェクトに保持します。

ドライバーが読み込まれると、ドライバーオブジェクトへのポインターを使用して[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンが呼び出されます。 ドライバーの**driverentry**ルーチンが呼び出されると、次のように、*ディスパッチ*、 *StartIo* (存在する場合)、および*アンロード*(存在する場合) を設定します。

```cpp
DriverObject->MajorFunction[IRP_MJ_xxx] = DDDispatchXxx; 
              :    : 
DriverObject->MajorFunction[IRP_MJ_yyy] = DDDispatchYyy; 
              :    : 
DriverObject->DriverStartIo = DDStartIo; 
DriverObject->DriverUnload = DDUnload; 
              :    : 
```

**Driverentry**ルーチンは、次のように、driver オブジェクトの**Driverentry**の*AddDevice*ルーチンのエントリポイントも設定します。

```cpp
DriverObject->DriverExtension->AddDevice = DDAddDevice; 
```

**Driverentry**またはオプションの[*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)ルーチンでは、ドライバーオブジェクトのフィールド ([ドライバーオブジェクトの図](introduction-to-driver-objects.md#driver-object-illustration)には示されていません) を使用して、configuration manager のレジストリデータベースの情報を取得したり、情報を設定したりすることもできます。 詳細については、「[ドライバーのレジストリキー](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)」を参照してください。

I/o マネージャーは、ドライバー [ **\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)構造であるドライバーオブジェクトを操作するためのサポートルーチンをエクスポートしません。 ドライバーオブジェクトは、現在読み込まれているドライバーを追跡するために、i/o マネージャーによって使用されます。 ドライバーオブジェクトの一部のメンバーは、i/o マネージャーによってのみ使用されます。 他のメンバーは、ドライバーライターによっても使用されます。たとえば、 *AddDevice*、 *Dispatch*、 *StartIo*、および*Unload*エントリポイントを定義するには、特定のメンバー名を把握しておく必要があります。 このドキュメントで名前が付けられているドライバーオブジェクトのメンバーの場所については、 **\_オブジェクト**構造では、ドキュメントに記載されていないメンバーを使用しないようにしてください。 そうしないと、1つの Windows プラットフォームから別の Windows プラットフォームへの移植性を維持することができません。

 

 





---
title: デバイス オブジェクトの作成
description: デバイス オブジェクトの作成
ms.assetid: 3eda8eb2-8a83-4753-a099-2531bfb9aeeb
keywords:
- デバイス オブジェクトの WDK カーネルを作成します。
- 非 WDM ドライバー デバイス オブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42923eb5e4ee1e112ed3d6957c53a4bba50565c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377182"
---
# <a name="creating-a-device-object"></a>デバイス オブジェクトの作成





モノリシック ドライバーでは、各物理、論理、または仮想デバイスの I/O 要求を処理対象のデバイス オブジェクトを作成する必要があります。 デバイスのデバイス オブジェクトを作成していないドライバーは、デバイスの任意の Irp を受信しません。

一部のテクノロジ領域で、クラス ドライバーまたはポート ドライバーに関連付けられているミニドライバーは、独自のデバイス オブジェクトを作成ありません。 代わりに、クラスまたはポートのドライバーでは、デバイス オブジェクトを作成し、デバイスのすべての Irp を受信します。 クラスまたはポートのドライバーは、このドライバー固有のメソッドを使用し、I/O 要求をミニドライバーに渡します。 Microsoft は、ドライバーの代わりのデバイス オブジェクトを作成するクラスまたはポートのドライバーを提供する、特定のテクノロジ領域のマニュアルを参照してください。

ドライバーは、いずれかを呼び出す[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)または[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)それらのデバイス オブジェクトを作成します。 使用するには、どのルーチンの詳細については、次のセクションを参照してください。

[WDM 関数とフィルター ドライバーのデバイス オブジェクトを作成します。](#creating-device-objects-for-wdm-function-and-filter-drivers)

[WDM バス ドライバーのデバイス オブジェクトを作成します。](#creating-device-objects-for-wdm-bus-drivers)

[非 WDM ドライバーのデバイス オブジェクトを作成します。](#creating-device-objects-for-non-wdm-drivers)

ドライバーは、デバイス オブジェクトを作成するときに次の情報を提供**IoCreateDevice**または**IoCreateDeviceSecure**:

-   デバイスのサイズ*デバイス拡張機能*します。 デバイスの拡張機能は、デバイスに固有の記憶域のドライバーが使用できるシステムによって割り当てられたストレージ領域です。 詳細については、次を参照してください。[デバイス拡張機能](device-extensions.md)します。

-   システム定義の定数を示す、 **DeviceType**デバイス オブジェクトによって表されます。 詳細については、次を参照してください。[デバイスの種類の指定](specifying-device-types.md)します。

-   1 つ以上の論理和、デバイスのデバイスの特性を示すシステム定義の定数。 詳細については、次を参照してください。[デバイスの特性を指定する](specifying-device-characteristics.md)します。

-   という名前のブール値*排他*を指定するか、デバイス オブジェクトのビットで**フラグ**で設定する必要があります\_排他、ドライバーなど、排他的なデバイスのサービスを示すビデオ、シリアル、パラレル、またはサウンド デバイスです。 WDM ドライバーを設定する必要があります*排他*に**FALSE**します。 詳細については、次を参照してください。[デバイス オブジェクトに排他アクセスを指定する](specifying-exclusive-access-to-device-objects.md)します。

-   ドライバーのドライバー オブジェクトへのポインター。 WDM 関数またはフィルター ドライバーでは、ドライバー、そのオブジェクトへのポインターを受け取るパラメーターとしてその[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。 すべてのドライバーがドライバー オブジェクトへのポインターを受け取る、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。 システムでは、このポインターを使用して、ドライバーをそのデバイス オブジェクトに関連付けます。

-   Null で終わる Unicode 文字列に省略可能なポインター (*DeviceName*) デバイスの名前を付けします。 WDM ドライバー、バス ドライバー、以外は、デバイス名を指定しません。そのため、これには、PnP マネージャーのセキュリティ機能がバイパスされます。 詳細については、次を参照してください。[という名前のデバイス オブジェクト](named-device-objects.md)します。

場合に呼び出し[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)または[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)成功すると、I/O マネージャーは、デバイス オブジェクトのストレージを提供します自体と、すべての他のデータ構造のデバイス オブジェクトに関連付けられている場合などのデバイスの拡張機能は、ゼロで初期化します。

### <a name="creating-device-objects-for-wdm-function-and-filter-drivers"></a>WDM 関数とフィルター ドライバーのデバイス オブジェクトを作成します。

WDM ドライバー、バス ドライバー、以外を呼び出す**IoCreateDevice**それらのデバイス オブジェクトを作成します。 ほとんどの WDM ドライバー内からそれらのデバイス オブジェクトを作成する、 *AddDevice*ルーチン。 ドライブのレイアウト、Ioctl に対応する必要がありますディスク ドライバーなど、一部のドライバーを呼び出す**IoCreateDevice**ディスパッチ ルーチンから。

Windows Driver Kit (WDK) ドキュメントの種類に固有のセクションではデバイスの状態それ以外の場合、しない場合、ドライバーがそのデバイス オブジェクトを作成する必要があります、 *AddDevice*ルーチン。 詳細については、次を参照してください。 [、AddDevice ルーチンを記述](writing-an-adddevice-routine.md)します。

### <a name="creating-device-objects-for-wdm-bus-drivers"></a>WDM バス ドライバーのデバイス オブジェクトを作成します。

WDM バス ドライバーへの応答で新しいデバイスの列挙時に、PDO を作成し、 [ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)場合、要求リレーションシップの種類は**BusRelations**します。

次の規則は、バス ドライバーを呼び出すかどうかを判断**IoCreateDevice**または**IoCreateDeviceSecure**デバイス オブジェクトを作成します。

-   デバイスで使用できる場合*raw モード*、呼び出すことが必要があります**IoCreateDeviceSecure**します。

-   デバイスが raw モードではない場合、対応、バス ドライバーを使用**IoCreateDevice**または**IoCreateDeviceSecure**します。 **IoCreateDevice**バス上のデバイスの既定のシステム セキュリティが適切ですときに使用できます。**IoCreateDeviceSecure**より厳格なセキュリティ記述子を指定するために使用できます。 詳細については、次を参照してください。[デバイスへのアクセスを制御する](controlling-device-access.md)します。

### <a name="creating-device-objects-for-non-wdm-drivers"></a>非 WDM ドライバーのデバイス オブジェクトを作成します。

非 WDM ドライバーを使用して**IoCreateDevice**名前のないデバイス オブジェクトを作成して**IoCreateDeviceSecure**という名前のデバイス オブジェクトを作成します。 非 WDM ドライバーの名前のないデバイス オブジェクトが、ドライバーは通常、少なくとも 1 つの名前付きオブジェクトを作成する必要がありますので、ユーザー モードからアクセスできるに注意してください。

 

 





---
title: デバイス オブジェクトの作成
description: デバイス オブジェクトの作成
ms.assetid: 3eda8eb2-8a83-4753-a099-2531bfb9aeeb
keywords:
- デバイスオブジェクト WDK カーネル、作成
- 非 WDM ドライバーデバイスオブジェクト WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fe99c5247d6eae64ad2e3517f7a0622df6de977
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837017"
---
# <a name="creating-a-device-object"></a>デバイス オブジェクトの作成





モノリシックドライバーは、i/o 要求を処理する物理デバイス、論理デバイス、または仮想デバイスごとにデバイスオブジェクトを作成する必要があります。 デバイスのデバイスオブジェクトを作成しないドライバーは、デバイスの Irp を受信しません。

一部のテクノロジ分野では、クラスドライバーまたはポートドライバーに関連付けられているミニドライバーは、独自のデバイスオブジェクトを作成する必要はありません。 代わりに、クラスまたはポートドライバーがデバイスオブジェクトを作成し、デバイスのすべての Irp を受信します。 次に、クラスまたはポートドライバーは、ドライバー固有のメソッドを使用して、i/o 要求をミニドライバーに渡します。 ドライバーの代わりにデバイスオブジェクトを作成するクラスまたはポートドライバーを Microsoft が提供するかどうかを判断するには、特定のテクノロジ領域のドキュメントを参照してください。

ドライバーは、デバイスオブジェクトを作成するために、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)または[**Iocreateデバイス ecを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)呼び出します。 使用するルーチンの詳細については、次のセクションを参照してください。

[WDM 関数とフィルタードライバー用のデバイスオブジェクトの作成](#creating-device-objects-for-wdm-function-and-filter-drivers)

[WDM バスドライバー用のデバイスオブジェクトの作成](#creating-device-objects-for-wdm-bus-drivers)

[WDM 以外のドライバー用のデバイスオブジェクトの作成](#creating-device-objects-for-non-wdm-drivers)

ドライバーは、デバイスオブジェクトを作成するときに、 **IoCreateDevice**または**iocreate**に次の情報を提供します。

-   デバイスの*デバイス拡張機能*のサイズ。 デバイス拡張機能は、システムによって割り当てられたストレージ領域で、ドライバーはデバイス固有の記憶域に使用できます。 詳細については、「[デバイスの拡張機能](device-extensions.md)」を参照してください。

-   デバイスオブジェクトによって表される **(devicetype**を示すシステム定義の定数。 詳細については、「[デバイスの種類の指定](specifying-device-types.md)」を参照してください。

-   デバイスのデバイスの特性を示す、1つまたは複数の論理演算されたシステム定義定数。 詳細については、「[デバイスの特性の指定](specifying-device-characteristics.md)」を参照してください。

-   デバイスオブジェクトの**フラグ**のビットを排他\_に設定するかどうかを指定する、 *exclusive*という名前のブール値。この値は、ドライバーがビデオ、シリアル、パラレル、サウンドなどのデバイスを排他的に使用することを示します。 WDM ドライバーは、*排他的*に**FALSE**に設定する必要があります。 詳細については、「[デバイスオブジェクトへの排他アクセスの指定](specifying-exclusive-access-to-device-objects.md)」を参照してください。

-   ドライバーのドライバーオブジェクトへのポインター。 WDM 関数またはフィルタードライバーは、その[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンへのパラメーターとして、そのドライバーオブジェクトへのポインターを受け取ります。 すべてのドライバーは、ドライバーオブジェクトへのポインターを[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンで受け取ります。 システムはこのポインターを使用して、ドライバーをそのデバイスオブジェクトに関連付けます。

-   デバイスに名前を付ける null で終わる Unicode 文字列 (*DeviceName*) へのポインター (省略可能)。 バスドライバー以外の WDM ドライバーでは、デバイス名が指定されていません。これにより、PnP マネージャーのセキュリティ機能がバイパスされます。 詳細については、「[名前付きデバイスオブジェクト](named-device-objects.md)」を参照してください。

[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)または[**iocreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)の呼び出しが成功した場合、i/o マネージャーは、デバイスオブジェクト自体およびデバイスオブジェクトに関連付けられているその他すべてのデータ構造 (デバイス拡張機能を含む) のストレージを提供します。0で初期化します。

### <a name="creating-device-objects-for-wdm-function-and-filter-drivers"></a>WDM 関数とフィルタードライバー用のデバイスオブジェクトの作成

バスドライバー以外の WDM ドライバーは、 **IoCreateDevice**を呼び出して、デバイスオブジェクトを作成します。 ほとんどの WDM ドライバーは、 *AddDevice*ルーチン内からデバイスオブジェクトを作成します。 ドライブレイアウトの Ioctl に応答する必要があるディスクドライバーなど、一部のドライバーは、ディスパッチルーチンから**IoCreateDevice**を呼び出します。

Windows Driver Kit (WDK) のドキュメント状態のデバイスの種類に固有のセクションを除き、ドライバーは、そのデバイスオブジェクトを*AddDevice*ルーチンに作成する必要があります。 詳細については、「 [AddDevice ルーチンの記述](writing-an-adddevice-routine.md)」を参照してください。

### <a name="creating-device-objects-for-wdm-bus-drivers"></a>WDM バスドライバー用のデバイスオブジェクトの作成

WDM バスドライバーは、IRP\_に応答して新しいデバイスを列挙するときに PDO を作成します。これは、関係の種類が**Busrelations**の場合、[**デバイス\_の関係要求\_\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)を実行します。

次の規則は、バスドライバーが**IoCreateDevice**または**iocreatestype**を呼び出してデバイスオブジェクトを作成するかどうかを決定します。

-   デバイスを*raw モード*で使用できる場合は、 **iocreateデバイス**を呼び出す必要があります。

-   デバイスが raw モードに対応していない場合、バスドライバーは、 **IoCreateDevice**または**iocreatestype**のどちらかを使用できます。 **IoCreateDevice**は、バス上のデバイスの既定のシステムセキュリティが適切な場合に使用できます。**Iocreateデバイス**を使用すると、より厳格なセキュリティ記述子を指定できます。 詳細については、「[デバイスアクセスの制御](controlling-device-access.md)」を参照してください。

### <a name="creating-device-objects-for-non-wdm-drivers"></a>WDM 以外のドライバー用のデバイスオブジェクトの作成

非 WDM ドライバーでは、 **IoCreateDevice**を使用して名前のないデバイスオブジェクトを作成し、 **iocreate**を使用して名前付きデバイスオブジェクトを作成します。 非 WDM ドライバーの名前のないデバイスオブジェクトにはユーザーモードからアクセスできないので、ドライバーは通常、少なくとも1つの名前付きオブジェクトを作成する必要があります。

 

 





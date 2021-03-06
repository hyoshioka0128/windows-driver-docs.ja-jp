---
title: 静的な列挙
description: 静的な列挙
ms.assetid: 58377f17-a9dc-4096-af23-36f8d8dbb87e
keywords:
- 静的列挙 WDK KMDF
- 静的な子 WDK KMDF を一覧表示します。
- 静的な子を走査 WDK KMDF を一覧表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d865a356980ffff0e903109c4c5678ec047f4005
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385956"
---
# <a name="static-enumeration"></a>静的な列挙


*列挙体の静的*は検出し、システムの構成に後続の変更を報告する機能が制限を使用したシステムの初期化中にデバイスの存在をレポートするドライバーの機能です。

バス ドライバーは、デバイスまたは機能のサブユニットの種類と数が事前に定義されたと永続的なおよびドライバーが実行されているシステムの構成に依存しない場合、静的列挙型を使用できます。

たとえば、サウンド カードのドライバーは、バス ドライバーとして機能し、カードのジョイスティックや MIDI、オーディオなどの機能ごとに個別の物理デバイス オブジェクト (Pdo) を作成します。

### <a name="static-child-lists"></a>静的な子リスト

フレームワークは、静的な子のリストを提供することで静的な列挙をサポートするドライバーを使用できます。 各静的子リストは、親デバイスに接続されている子デバイスの一覧を表します。 親デバイス用のバス ドライバーでは、親の子のデバイスを識別、親デバイスの静的な子の一覧に追加、および子デバイスごとの PDO を作成する必要があります。

### <a name="creating-a-static-child-list"></a>静的な子のリストを作成します。

ドライバーは、デバイスの機能のデバイス オブジェクト (FDO) を表す framework デバイス オブジェクトを作成するたびに、フレームワークに、デバイスの一覧を空の静的な子を作成します。

ときに、フレームワークがバス ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数では、コールバック関数を呼び出す必要があります[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)FDO 親デバイスを作成します。 FDO の作成の詳細については、次を参照してください。 [Function ドライバーのデバイス オブジェクトの作成](creating-device-objects-in-a-function-driver.md)です。

ドライバーする必要があります親デバイスの子の列挙、子の Pdo を作成し、子リストに、子を追加します。

ドライバーを呼び出すことができます必要に応じて、 [ **WdfDeviceSetBusInformationForChildren** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetbusinformationforchildren)バスについての情報をフレームワークを提供します。 子デバイスと、バスを識別するためにアプリを簡単になりますので、これをお勧めします。

子が検出されたデバイスの PDO を作成するには、バス ドライバー必要があります。

1.  呼び出す[ **WdfPdoInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)を取得する、 [ **WDFDEVICE\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体。

2.  初期化、WDFDEVICE\_INIT 構造体。

3.  呼び出す[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate) PDO を表す framework デバイス オブジェクトを作成します。

PDO の作成の詳細については、次を参照してください。[バス ドライバーのデバイス オブジェクトを作成する](creating-device-objects-in-a-bus-driver.md)します。

呼び出した後**WdfDeviceCreate**、ドライバーを呼び出す必要があります[ **WdfFdoAddStaticChild** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoaddstaticchild)子デバイスを子リストに追加します。

### <a name="modifying-a-static-child-list"></a>静的な子のリストを変更します。

のみ、ドライバーは事前に定義されたと永続的なデバイス構成の静的子リストを使用する必要があります、ためには、作成した後、子の静的リストを変更するためのドライバーのほとんどの必要がありません。 ドライバーを呼び出すことができる場合、ドライバーは、子デバイスがアクセス不能になったことを決定します、 [ **WdfPdoMarkMissing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdomarkmissing)します。 (子デバイスがアクセスできる状態応答しなかったり、使用不可になる場合に、ドライバーを設定する必要があります、 **Failed**のメンバー、 [ **WDF\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_state)構造体を**WdfTrue**を呼び出して[ **WdfDeviceSetDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate))。

### <a name="traversing-a-static-child-list"></a>静的な子リスト内の移動

静的子リストの内容を取得する必要がある場合、ドライバーは、次の手順を実行して、リストを走査できます。

1.  呼び出す[ **WdfFdoLockStaticChildListForIteration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdolockstaticchildlistforiteration)します。

2.  呼び出す[ **WdfFdoRetrieveNextStaticChild** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoretrievenextstaticchild)必要な回数だけです。

3.  呼び出す[ **WdfFdoUnlockStaticChildListFromIteration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdounlockstaticchildlistfromiteration)します。

 

 






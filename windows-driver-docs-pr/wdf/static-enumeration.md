---
title: 静的な列挙
description: 静的な列挙
ms.assetid: 58377f17-a9dc-4096-af23-36f8d8dbb87e
keywords:
- 静的な列挙型 WDK KMDF
- 静的な子リスト WDK KMDF
- 静的な子リストの走査 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f702fb8aff22665d4c9e441ea1d9cce611d098bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845191"
---
# <a name="static-enumeration"></a>静的な列挙


*静的列挙*は、システムの初期化中にデバイスの存在を検出して報告するドライバーの機能であり、システムの構成に対する後続の変更を報告する機能は限られています。

バスドライバーは、デバイスまたは機能サブユニットの数と種類が事前に設定され、永続的であり、ドライバーが実行されているシステムの構成に依存していない場合に、静的な列挙を使用できます。

たとえば、サウンドカードのドライバーはバスドライバーとして機能し、MIDI、オーディオ、ジョイスティックなどのカードの機能ごとに個別の物理デバイスオブジェクト (PDOs) を作成することができます。

### <a name="static-child-lists"></a>静的な子リスト

フレームワークを使用すると、静的な子リストを提供することで、ドライバーが静的列挙をサポートできるようになります。 各静的な子リストは、親デバイスに接続されている子デバイスの一覧を表します。 親デバイスのバスドライバーは、親の子デバイスを識別し、親デバイスの静的子リストに追加して、子デバイスごとに PDO を作成する必要があります。

### <a name="creating-a-static-child-list"></a>静的な子リストの作成

デバイスの機能デバイスオブジェクト (FDO) を表すフレームワークデバイスオブジェクトをドライバーが作成するたびに、フレームワークによってデバイスの空の静的子リストが作成されます。

フレームワークがバスドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を呼び出す場合、コールバック関数は[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、親デバイスの FDO を作成する必要があります。 FDO の作成の詳細については、「[関数ドライバーでのデバイスオブジェクトの作成](creating-device-objects-in-a-function-driver.md)」を参照してください。

次に、ドライバーは親デバイスの子を列挙し、子の PDOs を作成し、子リストに子を追加する必要があります。

必要に応じて、ドライバーは[**WdfDeviceSetBusInformationForChildren**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetbusinformationforchildren)を呼び出して、バスに関する情報をフレームワークに提供できます。 これを行うことをお勧めします。これにより、子デバイスとアプリがバスを識別しやすくなります。

検出された子デバイスの PDO を作成するには、バスドライバーで次のことを行う必要があります。

1.  [**Wdfpdoinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)を呼び出して、 [**wdfdevice\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体を取得します。

2.  WDFDEVICE\_INIT 構造体を初期化します。

3.  [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、PDO を表すフレームワークデバイスオブジェクトを作成します。

PDO の作成の詳細については、「[バスドライバーでのデバイスオブジェクトの作成](creating-device-objects-in-a-bus-driver.md)」を参照してください。

**WdfDeviceCreate**を呼び出した後、ドライバーは[**Wdffdoaddstaticchild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoaddstaticchild)を呼び出して子デバイスを子リストに追加する必要があります。

### <a name="modifying-a-static-child-list"></a>静的な子リストの変更

ドライバーは、事前に決められた永続的なデバイス構成の静的な子リストのみを使用する必要があるため、ドライバーを作成した後に静的子リストを変更する必要はほとんどありません。 子デバイスがアクセス不能になったとドライバーが判断した場合、ドライバーは[**Wdfpdomarkmissing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdomarkmissing)を呼び出すことができます。 (子デバイスはアクセス可能な状態で、応答不能になり、使用できなくなった場合、ドライバーは、 [**WDF\_device\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_state)構造の**失敗した**メンバーを**Wdftrue**に設定し、 [**wdfdevicesetdevicestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)を呼び出します)。

### <a name="traversing-a-static-child-list"></a>静的な子リストの走査

静的な子リストの内容を取得する必要がある場合、ドライバーは次の操作を行って一覧を走査できます。

1.  [**Wdffdolockstaticchildlistforiteration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdolockstaticchildlistforiteration)を呼び出しています。

2.  [**WdfFdoRetrieveNextStaticChild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoretrievenextstaticchild)の呼び出しは必要に応じて何回でも行うことができます。

3.  [**Wdffdounlockstaticchildlistfromiteration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdounlockstaticchildlistfromiteration)を呼び出しています。

 

 






---
title: ミニドライバーと HID クラス ドライバー
description: HID クラスドライバーの操作
ms.assetid: 3A8F5545-F8EB-47E2-989D-7DE83E32110E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2a69560e7e02e43547bfa7f0c327167eb614dc7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841573"
---
# <a name="minidrivers-and-the-hid-class-driver"></a>ミニドライバーと HID クラス ドライバー


このセクションには、HID クラスドライバーの操作に関する次のトピックが含まれています。

-   HID クラスドライバーの操作機能
-   Hid クラスドライバーの操作を HID ミニドライバーにバインドする
-   HID ミニドライバーとの通信

詳細については、「 [WDF HID ミニドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers)」を参照してください。

### <a name="operational-features-of-the-hid-class-driver"></a>HID クラスドライバーの操作機能

HID クラスドライバーは、次のことを行います。

-   カーネルモードドライバーとユーザーモードアプリケーションが、入力デバイスがサポートする[HID コレクション](hid-collections.md)にアクセスするために使用する、上位レベルのインターフェイスを提供し、管理します。

    HID クラスドライバーは、上位レベルのドライバーとアプリケーションと、HID コレクションをサポートする基になる入力デバイスとの間のすべての通信を透過的に管理し、ルーティングします。 異なる入力デバイスで使用されるさまざまなデータプロトコルと、同じ HID コレクションで複数の開いているファイルをサポートする入力キューを管理します。

    HID コレクションに対する上位レベルのインターフェイスは、 [hid クラスドライバーの ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)、 [HIDClass のサポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)、および[HIDClass 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)で構成されています。

-   ミニドライバーの標準ドライバールーチンを呼び出すことによって、HID ミニドライバーと通信します。

-   下位レベルのバスまたはポートドライバーによって列挙された HIDClass 入力デバイス用の機能デバイスオブジェクト (*FDO*) を作成します。

    たとえば、HID クラスドライバーは、システムによって提供される USB ドライバースタックによって列挙される USB HID デバイスを表す FDO の操作を作成し、管理します。

-   基になる入力デバイスでサポートされている子デバイス (HID コレクション) 用のバスドライバーの機能を提供します。

    HID クラスドライバーは、入力デバイスでサポートされている各 HID コレクション用に物理デバイスオブジェクト (*PDO*) を作成し、コレクションの操作を管理します。

### <a name="binding-a-minidriver-to-hidclass"></a>ミニドライバーを HIDClass にバインドする

Hid ミニドライバーは、その操作を hid クラスドライバーにバインドします。そのためには、 [**HidRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)を呼び出して hid クラスドライバーに登録します。 登録操作では、次の処理が行われます。

-   Hid クラスドライバーのデバイス拡張機能で、エントリポイント (ポインター) のコピーを HID ミニドライバーの標準ドライバールーチンに保存します。

    HID ミニドライバーは、ミニドライバーが[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンへの入力として受信するドライバーオブジェクト内のエントリポイントを設定します。 HID ミニドライバーは、HID クラスドライバーに登録する前に、これらのエントリポイントを設定します。

-   ミニドライバーの driver オブジェクトのエントリポイントを、HID クラスドライバーによって提供される標準ドライバールーチンのエントリポイントにリセットします。

HID クラスドライバーには、次の標準ドライバールーチンが用意されています。

-   [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)および[*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチン

-   次の i/o 要求のディスパッチルーチン:

    [**IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)

    [**IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

    [**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)

    [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)

    [**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

    [**IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)

また、登録プロセスでは、HID mindriver デバイス拡張機能にメモリが割り当てられます。 メモリは HID クラスドライバーによって割り当てられますが、このデバイス拡張機能を使用するのは HID ミニドライバーだけです。

### <a name="communicating-with-a-hid-minidriver"></a>HID ミニドライバーとの通信

Hid クラスドライバーは、次のように HID ミニドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)、 [*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)、および dispatch ルーチンを呼び出すことによって、hid ミニドライバーと通信します。

### <a name="calling-the-adddevice-routine"></a>AddDevice ルーチンの呼び出し

HID クラスドライバーの**AddDevice**ルーチンを呼び出して機能デバイスオブジェクト (*FDO*) を作成すると、hid クラスドライバーによって FDO が作成され、初期化され、hid ミニドライバー **AddDevice**ルーチンが呼び出されます。 HID ミニドライバー **AddDevice**ルーチンは、デバイス固有の内部初期化を実行します。成功した場合、状態\_SUCCESS を返します。 HID ミニドライバー **AddDevice**ルーチンが正常に実行されなかった場合、hid クラスドライバーは FDO を削除し、Hid ミニドライバー **AddDevice**ルーチンによって返された状態を返します。

### <a name="calling-the-unload-routine"></a>アンロードルーチンの呼び出し

HID クラスドライバーの**アンロード**ルーチンが呼び出されると、hid クラスドライバーは、FDO に関連付けられているすべてのリソースの解放を完了し、hid ミニドライバーの**アンロード**ルーチンを呼び出します。

### <a name="calling-the-dispatch-routines"></a>ディスパッチルーチンの呼び出し

デバイスを操作するために、HID クラスドライバーは、主にデバイスコントロールの内部要求に対して HID ミニドライバー dispatch ルーチンを呼び出します。

また、i/o マネージャーがプラグアンドプレイ、power、またはシステム制御要求を FDO の HID クラスドライバーに送信すると、HID クラスドライバーによって要求が処理され、HID ミニドライバーの対応するディスパッチルーチンが呼び出されます。

HID クラスドライバーは、次の要求を HID ミニドライバー (作成、クローズ、デバイスコントロール) に送信しません。

### <a name="operation-of-a-hid-minidriver"></a>HID ミニドライバーの操作

HID transport ミニドライバーは、入力デバイスが接続するハードウェアバスまたはポートの操作を抽象化します。

HID ミニドライバーは、次のいずれかのフレームワークを使用して構築できます。

-   UMDF –ユーザーモードドライバーフレームワーク
-   KDMF –カーネルモードドライバーフレームワーク
-   WDM –レガシ Windows Driver Model

Microsoft では、フレームワークベースのソリューション (Windows 8 のみ) を使用することをお勧めします。 各ドライバーモデルの詳細については、次のセクションを参照してください。

-   KMDF ベースの HID ミニドライバー、「フレームワークベースの HID ミニドライバーの作成」を参照してください。
-   UMDF ベースの HID ミニドライバー、「UMDF ベースの HID ミニドライバーの作成」を参照してください。

次のセクションでは、WDM ベースの HID ミニドライバーの登録について説明しますが、その多くは KMDF ベースのフレームワークドライバーにも関係しています。 すべての HID ミニドライバーは HID クラスドライバーに登録する必要があり、HID クラスドライバーはミニドライバーの標準ドライバールーチンを呼び出すことによってミニドライバーと通信します。

標準のドライバールーチンで HID ミニドライバーがサポートする必要がある機能の詳細については、次のトピックを参照してください。

-   HID ミニドライバーの登録
-   HID ミニドライバードライバーの拡張機能
-   HID\_デバイス\_拡張構造の使用
-   HID ミニドライバーによって提供される標準ドライバールーチン

HID クラスドライバーの詳細については、「HID クラスドライバーの操作」を参照してください。

### <a name="registering-a-hid-minidriver"></a>HID ミニドライバーの登録

HID ミニドライバーが[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンで他のすべてのドライバー初期化を完了すると、hid ミニドライバーは[**HidRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)を呼び出してその操作を hid クラスドライバーにバインドします。

Hid ミニドライバーが HID クラスドライバーに登録すると、hid のリビジョン、HID ミニドライバー driver オブジェクト、HID ミニドライバー device extension のサイズを指定するために、 [**hid\_ミニドライバー\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/ns-hidport-_hid_minidriver_registration)構造を使用します。デバイスをポーリングするかどうかを指定します。

### <a name="hid-minidriver-extension"></a>HID ミニドライバー拡張機能

HID ミニドライバーデバイス拡張機能はデバイスに固有であり、HID ミニドライバーによってのみ使用されます。 HID クラスドライバーは、クラスドライバーが機能デバイスオブジェクト (*FDO*) のデバイス拡張機能を作成するときに、ミニドライバーデバイス拡張機能のメモリを割り当てます。 Hid ミニドライバーは、ミニドライバーを HID クラスドライバーに登録するときのデバイス拡張機能のサイズを指定します。 サイズは、 [**HID\_ミニドライバー\_の登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/ns-hidport-_hid_minidriver_registration)構造の**deviceextensionsize**メンバーによって指定されます。

### <a href="" id="using-the-hid-device-extension-structure"></a>HID\_デバイス\_拡張構造の使用

HID ミニドライバーは、 **hid\_デバイス\_拡張機能**) を使用する必要があります。 HID クラスドライバーは、FDO を初期化するときに、この構造体のメンバーを設定します。 HID ミニドライバーは、この構造の情報を変更することはできません。

HID\_デバイス\_の拡張構造には、次のメンバーが含まれています。

-   **PhysicalDeviceObject**は、基になる入力デバイスを表す物理デバイスオブジェクト (PDO) へのポインターです。

-   **NextDeviceObject**は、FDO の下にあるデバイススタックの一番上にあるポインターです。

-   **Minideviceextension**は、HID ミニドライバー device 拡張機能へのポインターです。

入力デバイスの FDO へのポインターを指定すると、次の GET\_ミニドライバー\_DEVICE\_EXTENSION マクロは、HID ミニドライバー extension へのポインターを返します。

```cpp
#define GET_MINIDRIVER_DEVICE_EXTENSION(DO) ((PDEVICE_EXTENSION) (((PHID_DEVICE_EXTENSION)(DO)->DeviceExtension)->MiniDeviceExtension))
```

PDEVICE\_EXTENSION は、HID ミニドライバーによって宣言されたデバイス固有のデバイス拡張機能へのポインターです。

同様に、HID ミニドライバーは、入力デバイスの PDO へのポインターと、入力デバイスの FDO の下にあるデバイススタックの先頭を取得できます。

HID ミニドライバーがデバイススタックから IRP を送信する場合、ターゲットデバイスオブジェクトとして**NextDeviceObject**を使用する必要があります。

### <a name="standard-minidriver-routines"></a>標準ミニドライバールーチン

HID ミニドライバーは、次の標準ドライバーサポートルーチンを提供する必要があります。

-   HID ミニドライバー DriverEntry ルーチン
-   HID ミニドライバー AddDevice ルーチン
-   HID ミニドライバー Unload ルーチン

HID ミニドライバーは、「HID ミニドライバーによって提供されるディスパッチルーチン」で説明されているディスパッチルーチンもサポートする必要があります。

### <a name="driverentry-routine"></a>DriverEntry ルーチン

HID ミニドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンでは、次のことが行われます。

-   リンクされたドライバーのペア (HID クラスドライバーと HID ミニドライバー) のドライバーオブジェクトを作成します。

-   HID ミニドライバー driver オブジェクトに必要なドライバーエントリポイントを設定します。

-   [**HidRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)を呼び出して、hid ミニドライバーを hid クラスドライバーに登録します。

-   HID ミニドライバーによってのみ使用されるデバイス固有の構成を行います。

### <a name="adddevice-routine"></a>AddDevice ルーチン

HID クラスドライバーは、基になる入力デバイスの機能デバイスオブジェクト (*FDO*) の作成と初期化を処理します。 また、HID クラスドライバーは、上位レベルのインターフェイスから、基になるデバイスとその子デバイス (HID コレクション) への FDO を操作します。

HID クラスドライバー [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンは、ミニドライバーがデバイス固有の内部初期化を実行できるように、Hid ミニドライバー *AddDevice*ルーチンを呼び出します。

HID ミニドライバー [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンに渡されるパラメーターは、ミニドライバー driver オブジェクトおよび FDO です。 (HID クラスドライバーは、基になる入力デバイスの物理デバイスオブジェクトではなく、ミニドライバー *AddDevice*ルーチンに FDO を渡すことに注意してください)。

HID ミニドライバー [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンは、FDO からミニドライバーデバイス拡張機能へのポインターを取得します。

-   通常、HID ミニドライバー [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンは次のことを行います。

-   ミニドライバーデバイス拡張機能を初期化します。 デバイスの拡張機能は、ミニドライバーによってのみ使用されます。

-   ステータス\_成功を返します。 ミニドライバーがエラー状態を返した場合、HID クラスドライバーは FDO を削除し、エラー状態をプラグアンドプレイマネージャーに返します。

### <a name="unload-routine"></a>アンロードルーチン

HID クラスドライバーの Unload ルーチンは、HID ミニドライバー Unload ルーチンを呼び出します。 HID ミニドライバーは、ミニドライバーによって割り当てられたすべての内部リソースを解放します。

### <a name="dispatch-routines"></a>ディスパッチルーチン

HID ミニドライバーは、作成、終了、内部デバイスコントロール、システムコントロール、プラグアンドプレイ、電源管理の各ディスパッチルーチンを提供する必要があります。 内部デバイス制御要求を除き、これらのディスパッチルーチンのほとんどは最小限の機能を提供します。 HID クラスドライバーは、これらのディスパッチルーチンを呼び出すと、ミニドライバー driver オブジェクトと機能デバイスオブジェクト (*FDO*) を渡します。

### <a href="" id="irp-mj-create"></a>IRP\_MJ\_作成

WDM の要件に準拠して、HID クラスドライバーと HID ミニドライバーは、作成要求のディスパッチルーチンを提供します。 ただし、FDO は開くことができません。 HID クラスドライバーがステータス\_失敗したことを返します。

HID ミニドライバーはスタブのみを提供する必要があります。 Create dispatch ルーチンは呼び出されません。

### <a href="" id="irp-mj-close"></a>IRP\_MJ\_閉じる

WDM の要件に準拠して、HID クラスドライバーと HID ミニドライバーは、クローズ要求のディスパッチルーチンを提供する必要があります。 ただし、FDO は開くことができません。 HID クラスドライバーは、状態\_無効\_パラメーター\_1 を返します。

HID ミニドライバーはスタブのみを提供する必要があります。 Close ディスパッチルーチンは呼び出されません。

### <a href="" id="irp-mj-device-control"></a>IRP\_MJ\_デバイス\_コントロール

HID ミニドライバーは、デバイスコントロール要求のディスパッチルーチンを必要としません。 HID クラスドライバーは、デバイス制御要求をミニドライバーに渡しません。

### <a href="" id="irp-mj-internal-device-control"></a>IRP\_MJ\_内部\_デバイス\_コントロール

HID ミニドライバーは、 [Hid MinidriverIOCTLs](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)で説明されている要求をサポートする内部デバイス制御要求のディスパッチルーチンを提供する必要があります。

HID クラスドライバーは、主に、内部のデバイス制御要求を使用して、基になる入力デバイスにアクセスします。

HID ミニドライバーは、これらの要求をデバイス固有の方法で処理します。

### <a href="" id="irp-mj-system-control"></a>IRP\_MJ\_システム\_コントロール

HID ミニドライバーは、システム制御要求のディスパッチルーチンを提供する必要があります。 ただし、HID ミニドライバーは、次のように、デバイススタックからシステム制御要求を渡す場合にのみ必要です。

-   現在の IRP スタックの場所をスキップします

-   FDO のデバイススタックで要求を送信する

### <a href="" id="irp-mj-pnp"></a>IRP\_MJ\_PNP

HID ミニドライバーは、プラグアンドプレイ要求のディスパッチルーチンを提供する必要があります。

HID クラスドライバーは、FDO に関連付けられているすべてのプラグアンドプレイ処理を実行します。 HID クラスドライバーがプラグアンドプレイ要求を処理するときに、HID ミニドライバープラグアンドプレイディスパッチルーチンを呼び出します。

HID ミニドライバープラグアンドプレイディスパッチルーチンでは、次のことが行われます。

-   要求の種類ごとに必要に応じて、FDO のデバイススタックを介して要求を送信し、デバイススタックをバックアップする方法で要求を完了する処理を行います。

-   特定の要求に関連付けられているデバイス固有の処理で、FDO の状態に関する情報を更新します。

    たとえば、ミニドライバーは FDO のプラグアンドプレイ状態を更新する場合があります (特に、FDO が開始、停止、または削除中であるかどうか)。

### <a href="" id="irp-mj-power"></a>IRP\_MJ\_の電源

HID ミニドライバーは、電源要求のディスパッチルーチンを提供する必要があります。 ただし、HID クラスドライバーは、FDO の電力処理を処理します。

WDM の要件に準拠して、HID ミニドライバーは次の方法で、FDO のデバイススタックから電力要求を送信します。

-   現在の IRP スタックの場所をスキップします

-   次の電源 IRP を開始します

-   Power IRP を FDO のデバイススタックに送信します

通常、HID ミニドライバーは、追加の処理を行わずに、デバイススタックに電力要求を渡します。

 

 





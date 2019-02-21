---
title: ミニドライバーと HID クラス ドライバー
description: HID クラス ドライバーの操作
ms.assetid: 3A8F5545-F8EB-47E2-989D-7DE83E32110E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c9e0ae2cf19ed107445480cef430d4b13a61f02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559571"
---
# <a name="minidrivers-and-the-hid-class-driver"></a>ミニドライバーと HID クラス ドライバー


セクションには、HID クラス ドライバーの動作の詳細については、次のトピックが含まれています。

-   HID クラス ドライバーの運用機能
-   HID クラス ドライバーの動作を HID ミニドライバーにバインドします。
-   HID ミニドライバーとの通信

参照してください[WDF を非表示を作成するミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers)詳細についてはします。

### <a name="operational-features-of-the-hid-class-driver"></a>HID クラス ドライバーの運用機能

HID クラス ドライバーは、次を行います。

-   提供し、カーネル モード ドライバーとユーザー モード アプリケーションに使用する上位のインターフェイスの管理アクセス、 [HID コレクション](hid-collections.md)入力デバイスをサポートします。

    HID クラス ドライバーは透過的に管理し、上位レベルのドライバーとアプリケーションと HID コレクションをサポートする、基になる入力デバイス間のすべての通信をルーティングします。 さまざまな入力デバイスで使用されるさまざまなデータ プロトコルと同じ HID コレクションに対して 1 つ以上の開いているファイルをサポートする入力キューを管理します。

    HID コレクションに上位レベルのインターフェイスを構成、 [HID クラス ドライバーの Ioctl](https://msdn.microsoft.com/library/windows/hardware/ff539849)、 [HIDClass サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff538865)、および[HIDClass 構造](https://msdn.microsoft.com/library/windows/hardware/ff538854)。

-   ミニドライバーの標準のドライバーのルーチンを呼び出すことによって、HID ミニドライバーと通信します。

-   機能のデバイス オブジェクトを作成します (*FDO*) HIDClass の低レベル バスまたはポート ドライバーによって列挙されたデバイスを入力します。

    たとえば、HID クラス ドライバーは、作成し、システム提供の USB ドライバー スタックによって列挙 USB HID デバイスを表す FDO の操作を管理します。

-   基になる入力デバイスでサポートされている子デバイス (HID コレクション) のバス ドライバーの機能を提供します。

    HID クラス ドライバーは、物理デバイス オブジェクトを作成します (*PDO*) 各 HID のコレクションは、入力デバイスでサポートされているし、コレクションの操作を管理します。

### <a name="binding-a-minidriver-to-hidclass"></a>HIDClass へ、ミニドライバーのバインド

HID ミニドライバー HID クラス ドライバーを呼び出すことによって、操作をバインドする[ **HidRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff539835) HID クラス ドライバーを使用したそのものを登録します。 登録操作は、次を行います。

-   HID クラス ドライバーのデバイスの拡張機能の HID ミニドライバーの標準のドライバーのルーチンをエントリ ポイント (ポインター) のコピーを保存します。

    HID ミニドライバーでは、そのエントリ ポイントを設定、ミニドライバーをへの入力として受け取るドライバー オブジェクトでその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。 HID ミニドライバーは、HID クラス ドライバーに登録する前に、これらのエントリ ポイントを設定します。

-   HID クラス ドライバーによって提供される標準のドライバーのルーチンのエントリ ポイントにミニドライバーのドライバー オブジェクト内のエントリ ポイントをリセットします。

HID クラス ドライバーには、次の標準のドライバー ルーチンが用意されています。

-   [*AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)と[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチン

-   次の I/O 要求のディスパッチ ルーチン:

    [**IRP\_MJ\_CREATE**](https://msdn.microsoft.com/library/windows/hardware/ff550729)

    [**IRP\_MJ\_CLOSE**](https://msdn.microsoft.com/library/windows/hardware/ff550720)

    [**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550744)

    [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)

    [**IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)

    [**IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813)

また、登録プロセスは、HID mindriver デバイス拡張機能のメモリを割り当てます。 HID クラス ドライバーによって、メモリの割り当て、HID ミニドライバーだけでは、このデバイスの拡張機能を使用します。

### <a name="communicating-with-a-hid-minidriver"></a>HID ミニドライバーとの通信

HID クラス ドライバーは、HID ミニドライバーを呼び出すことによって、HID ミニドライバーと通信する[ *AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521)、 [*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)とディスパッチ次のようにルーチン:

### <a name="calling-the-adddevice-routine"></a>AddDevice ルーチンの呼び出し

ときに、HID クラス ドライバーの**AddDevice**ルーチンが機能するデバイス オブジェクトを作成すると呼ばれる (*FDO*)、HID クラス ドライバーが、FDO を作成し、それを初期化しますおよび HID ミニドライバーを呼び出す**AddDevice**ルーチン。 HID ミニドライバー **AddDevice**ルーチンはデバイス固有の内部初期化し、成功した場合、状態を返します\_成功します。 場合 HID ミニドライバー **AddDevice**ルーチンが成功しなかった場合、HID クラス ドライバーは、FDO を削除し、HID ミニドライバーによって返される状態を返します**AddDevice**ルーチン。

### <a name="calling-the-unload-routine"></a>アンロード ルーチンの呼び出し

HID class driver**アンロード**ルーチンが呼び出される、HID クラス ドライバーが FDO に関連付けられているすべてのリソースを解放が完了して、HID ミニドライバーの呼び出し、**アンロード**ルーチン。

### <a name="calling-the-dispatch-routines"></a>ディスパッチ ルーチンを呼び出す

デバイスを操作するには、HID クラス ドライバーは主に内部デバイス制御要求の HID ミニドライバー ディスパッチ ルーチンを呼び出します。

さらに、I/O マネージャーはプラグ アンド プレイ、電源、またはシステムのコントロール要求を FDO 用 HID クラス ドライバーに送信するときに、HID クラス ドライバーは、要求を処理し、HID ミニドライバーの対応するディスパッチ ルーチンを呼び出します。

HID クラス ドライバーは HID ミニドライバーに、次の要求を送信しません。 作成、close、またはデバイスを制御します。

### <a name="operation-of-a-hid-minidriver"></a>HID ミニドライバーの操作

HID のトランスポート ミニドライバーは、ハードウェア バスや入力デバイスの接続にポートの操作を抽象化します。

HID ミニドライバーは、次のフレームワークの 1 つを使用して構築できます。

-   UMDF – ユーザー モード ドライバー フレームワーク
-   KDMF – カーネル モード ドライバー フレームワーク
-   WDM – レガシ Windows Driver Model

フレームワーク ベースのソリューション (KMDF または (Windows 8 の場合のみ) の UMDF) を使用することをお勧めします。 各ドライバー モデルの詳細については、次のセクションを参照してください。

-   KMDF ベースの HID ミニドライバーは、HID ミニドライバーの作成のフレームワークに基づくを参照してください。
-   UMDF ベースの HID ミニドライバーは、HID ミニドライバーを作成する UMDF ベースを参照してください。

WDM の登録に関する次のセクションでベース HID ミニドライバーします、に関連するその大部分は、KMDF ベースのもフレームワーク ドライバー。 すべて HID ミニドライバーは、HID クラス ドライバーを登録する必要があり、ミニドライバーの標準のドライバーのルーチンを呼び出すことによって、HID クラス ドライバーが、ミニドライバーと通信します。

HID ミニドライバーは、その標準のドライバーのルーチンでサポートが必要な機能の詳細については、次のトピックを参照してください。

-   HID ミニドライバーを登録します。
-   HID ミニドライバー ドライバーの拡張機能
-   HID を使用して\_デバイス\_拡張機能の構造体
-   HID ミニドライバーによって提供される標準のドライバー ルーチン

HID クラス ドライバーの詳細については、HID クラス ドライバーの操作を参照してください。

### <a name="registering-a-hid-minidriver"></a>HID ミニドライバーを登録します。

ミニドライバーの内に他のドライバーのすべての初期化の完了後、HID その[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン、HID ミニドライバーの操作にバインド HID クラス ドライバーを呼び出して[ **HidRegisterMinidriver**](https://msdn.microsoft.com/library/windows/hardware/ff539835)します。

HID ミニドライバーは、HID クラス ドライバーを使用した登録を使用して、 [ **HID\_ミニドライバー\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff539929)構造体を次を指定します。HID リビジョン、HID ミニドライバー ドライバー オブジェクト、HID ミニドライバー デバイス拡張機能のサイズかどうかにデバイスをポーリングするかどうかとします。

### <a name="hid-minidriver-extension"></a>HID のミニドライバーの拡張機能

HID ミニドライバー デバイス拡張機能は、デバイスに固有では HID ミニドライバーでのみ使用します。 HID クラス ドライバー メモリを割り当てて、ミニドライバー デバイス拡張機能クラス ドライバーは、そのデバイスの拡張機能のデバイス オブジェクトを作成するときに (*FDO*)。 HID ミニドライバーは、HID クラス ドライバーを使用した、ミニドライバーを登録するときに、そのデバイスの拡張機能のサイズを指定します。 サイズが指定された、 **DeviceExtensionSize**のメンバー、 [ **HID\_ミニドライバー\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff539929)構造体。

### <a href="" id="using-the-hid-device-extension-structure"></a>HID を使用して\_デバイス\_拡張機能の構造体

非表示にするミニドライバーを使用する必要があります、 **HID\_デバイス\_拡張子**)。 HID クラス ドライバーは、FDO の初期化時にこの構造体のメンバーを設定します。 HID ミニドライバーは、この構造体で情報を変更する必要があります。

HID\_デバイス\_拡張機能の構造体には、次のメンバーが含まれています。

-   **PhysicalDeviceObject**物理デバイス (PDO) を表すオブジェクトを基になる入力デバイスへのポインターです。

-   **NextDeviceObject** FDO の下にあるデバイス スタックの一番上へのポインターです。

-   **MiniDeviceExtension** HID ミニドライバー デバイス拡張機能へのポインターです。

次の GET の入力デバイスの FDO にポインターを指定された\_ミニドライバー\_デバイス\_HID ミニドライバーの拡張機能に拡張機能のマクロのポインターを返します。

```cpp
#define GET_MINIDRIVER_DEVICE_EXTENSION(DO) ((PDEVICE_EXTENSION) (((PHID_DEVICE_EXTENSION)(DO)->DeviceExtension)->MiniDeviceExtension))
```

PDEVICE\_拡張機能は、HID ミニドライバーで宣言されているデバイスに固有のデバイスの拡張機能へのポインター。

同様に、HID ミニドライバーは、入力デバイスの PDO と、入力デバイスの FDO の下にあるデバイス スタックの一番上にポインターを取得できます。

HID ミニドライバーは、デバイス スタック IRP を送信するときに使用する**NextDeviceObject**対象のデバイス オブジェクトとして。

### <a name="standard-minidriver-routines"></a>標準のミニドライバー ルーチン

HID ミニドライバーは、次の標準のドライバー サポート ルーチンを提供する必要があります。

-   HID ミニドライバー DriverEntry ルーチン
-   HID ミニドライバー AddDevice ルーチン
-   HID ミニドライバー アンロード ルーチン

HID ミニドライバーは、HID ミニドライバー ディスパッチ ルーチンの提供で説明したディスパッチ ルーチンもサポートする必要があります。

### <a name="driverentry-routine"></a>DriverEntry ルーチン

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) HID ミニドライバーのルーチンは、次を実行します。

-   ドライバーのドライバー (HID クラス ドライバーおよび HID ミニドライバー) のリンクのペアを作成します。

-   HID ミニドライバー ドライバー オブジェクトに必要なドライバーのエントリ ポイントを設定します。

-   呼び出し[ **HidRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff539835) HID クラス ドライバーを使用した HID ミニドライバーを登録します。

-   HID ミニドライバーでのみ使用されるデバイス固有の構成を行います。

### <a name="adddevice-routine"></a>AddDevice ルーチン

HID クラス ドライバーは処理を作成して、機能のデバイス オブジェクトの初期化 (*FDO*) の基になる入力デバイス。 HID クラス ドライバーは、基になるデバイスとその子デバイス (HID コレクション) に、上位レベルのインターフェイスの観点から FDO も動作します。

HID クラス ドライバー [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンは、HID ミニドライバーを呼び出す*AddDevice*ルーチンのミニドライバーは、デバイス固有の内部の初期化を実行できるようにします。

HID ミニドライバーに渡されるパラメーター [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンは、ミニドライバー ドライバー オブジェクトと、FDO します。 (HID クラス ドライバーが、FDO をミニドライバーに渡すことに注意してください*AddDevice*日常的な、基になる入力デバイスの物理デバイス オブジェクトにありません。)。

HID ミニドライバー [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン、FDO からミニドライバー デバイス拡張機能にポインターを取得します。

-   HID ミニドライバーでは通常、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンは、次を実行します。

-   ミニドライバー デバイス拡張機能を初期化します。 デバイスの拡張機能は、ミニドライバーでのみ使用されます。

-   ステータスを返します\_成功します。 ミニドライバーはエラー状態を返す場合、HID クラス ドライバーは、FDO を削除し、プラグ アンド プレイのマネージャーに、エラー状態を返します。

### <a name="unload-routine"></a>ルーチンをアンロードします。

HID クラス ドライバーのアンロードのルーチンでは、HID ミニドライバー アンロード ルーチンを呼び出します。 HID ミニドライバーは、ミニドライバーによって割り当てられている内部リソースを解放します。

### <a name="dispatch-routines"></a>ディスパッチ ルーチン

HID ミニドライバーは、次のディスパッチ ルーチンを指定する必要があります。 閉じるには、内部のデバイスの制御、システムの制御、プラグ アンド プレイ、および電源管理を作成します。 内部デバイス制御の要求を除き、これらのディスパッチ ルーチンのほとんどは最小限の関数を提供します。 HID クラス ドライバーがこれらのディスパッチ ルーチンを呼び出すとき、ミニドライバー ドライバー オブジェクトと機能のデバイス オブジェクトに渡します (*FDO*)。

### <a href="" id="irp-mj-create"></a>IRP\_MJ\_CREATE

WDM の要件に準拠している、HID クラス ドライバーと HID ミニドライバーは作成要求のディスパッチ ルーチンを提供します。 ただし、FDO を開くことができません。 HID クラス ドライバーのステータスを返します\_失敗しました。

HID ミニドライバーは、スタブを提供するだけです。 作成ディスパッチ ルーチンは呼び出されません。

### <a href="" id="irp-mj-close"></a>IRP\_MJ\_閉じる

WDM の要件に準拠している、HID クラス ドライバーと HID ミニドライバーは閉じる要求のディスパッチ ルーチンを提供する必要があります。 ただし、FDO を開くことができません。 HID クラス ドライバーのステータスを返します\_無効な\_パラメーター\_1。

HID ミニドライバーは、スタブを提供するだけです。 閉じるディスパッチ ルーチンは呼び出されません。

### <a href="" id="irp-mj-device-control"></a>IRP\_MJ\_デバイス\_コントロール

HID ミニドライバーは、デバイス制御要求のディスパッチ ルーチンを必要はありません。 HID クラス ドライバーは、デバイス制御要求をミニドライバーにパスしません。

### <a href="" id="irp-mj-internal-device-control"></a>IRP\_MJ\_内部\_デバイス\_コントロール

HID ミニドライバーで説明されている要求をサポートする内部デバイス制御要求のディスパッチ ルーチンを提供する必要があります[HID MinidriverIOCTLs](https://msdn.microsoft.com/library/windows/hardware/ff539926)します。

主に、HID クラス ドライバーは、基になる入力デバイスにアクセスするのに内部デバイス制御要求を使用します。

HID ミニドライバーは、デバイス固有の方法でこれらの要求を処理します。

### <a href="" id="irp-mj-system-control"></a>IRP\_MJ\_システム\_コントロール

HID ミニドライバーは、システムのコントロール要求のディスパッチ ルーチンを提供する必要があります。 ただし、HID ミニドライバーがシステム デバイス スタックに対する制御要求を次のように渡す必要のみです。

-   IRP スタックの現在の場所をスキップします。

-   FDO のデバイス スタック ダウン要求を送信します。

### <a href="" id="irp-mj-pnp"></a>IRP\_MJ\_PNP

HID ミニドライバーは、プラグ アンド プレイの要求のディスパッチ ルーチンを指定する必要があります。

HID クラス ドライバーは、FDO に関連付けられているすべてのプラグ アンド プレイ処理を実行します。 HID クラス ドライバーがプラグ アンド プレイの要求を処理するときに、HID ミニドライバーのプラグ アンド プレイのディスパッチ ルーチンを呼び出します。

HID ミニドライバーのプラグ アンド プレイのディスパッチ ルーチンは、次を行います。

-   FDO のデバイス スタックを要求を送信し、途中で要求を完了するハンドルは、要求の種類ごとに、必要に応じて、デバイス スタックをバックアップします。

-   FDO の状態に関する情報を更新する特定の要求に関連付けられているデバイスに固有の処理を実行するには。

    たとえば、(、FDO を開始すると、停止、かどうかに具体的には、または削除処理中)、ミニドライバーは、FDO のプラグ アンド プレイ状態を更新可能性があります。

### <a href="" id="irp-mj-power"></a>IRP\_MJ\_電源

HID ミニドライバーは、電源の要求のディスパッチ ルーチンを指定する必要があります。 ただし、HID クラス ドライバーは、FDO の処理能力を処理します。

WDM の要件に準拠しているは、HID ミニドライバーは、次のように FDO のデバイスのスタックに power の要求を送信します。

-   IRP スタックの現在の場所をスキップします。

-   [次へ] のパワー IRP を開始します。

-   FDO のデバイス スタック電源 IRP を送信します。

通常、HID ミニドライバーは、追加の処理を行わなくてもデバイス スタック power 要求を渡します。

 

 





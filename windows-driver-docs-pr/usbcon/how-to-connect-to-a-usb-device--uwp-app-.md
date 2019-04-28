---
Description: Windows 8.1 では、USB デバイスと対話する UWP アプリを記述できます。
title: USB デバイスへの接続方法 (UWP アプリ)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5eca6881309b15cda4619af2df05e708a826aa7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364826"
---
# <a name="how-to-connect-to-a-usb-device-uwp-app"></a>USB デバイスへの接続方法 (UWP アプリ)


**概要**

-   使用する方法、 [ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)デバイスを検出するオブジェクト
-   通信用にデバイスを開く方法
-   使用してこれが完了したら、デバイスを閉じる方法

**重要な API**

-   [**UsbDevice**](https://msdn.microsoft.com/library/windows/apps/dn263883)
-   [**DeviceWatcher**](https://msdn.microsoft.com/library/windows/apps/br225446)

USB デバイスと対話する UWP アプリを記述するときに、アプリことができます制御コマンドを送信、デバイスの情報を取得し、読み取りおよび書き込み一括および割り込みのエンドポイントとの間のデータ。 すべての操作を行うことができます、前にデバイスを検出し、接続を確立する必要があります。

## <a name="before-you-start"></a>はじめに...


-   これは、一連の最初のトピックです。 このチュートリアルを開始する前に、このチュートリアルでは拡張可能な基本的な Visual Studio プロジェクトを作成する必要があります。 読み取り[UWP アプリの概要](https://go.microsoft.com/fwlink/p/?linkid=617681)の詳細。
-   コード例は、CustomUsbDeviceAccess サンプルに基づいています。 完全なサンプルは、このコード ギャラリーのページからダウンロードできます。
-   チュートリアルで使用する USB デバイスは、SuperMUTT デバイスです。
-   使用するには、 [ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466) USB デバイス、デバイスと連携する Windows アプリを作成する名前空間は、その関数のドライバーとして読み込まれます Winusb.sys のドライバーを使用する必要があります。 Winusb.sys が Microsoft によって提供されでの Windows に含まれている、  **\\Windows\\System32\\ドライバー**フォルダー。

## <a name="flowchart-finding-the-device"></a>フローチャート:デバイスの検索


USB デバイスに接続するには、最初の検出のさまざまなパターンに基づいてデバイスを検索しに接続しする必要があります。

-   特定のデバイス インターフェイスの GUID を持つ任意の USB デバイスに接続します。
-   ベンダー ID と製品 ID は、特定の USB デバイスに接続して、特定のデバイス インターフェイスの GUID を持ちます。
-   USB デバイスに特定のベンダー ID と製品 ID を知らなくても接続デバイス インターフェイスの GUID。
-   デバイスのクラスが知られている USB デバイスに接続します。

![usb デバイスの検出](images/scenario1-flowchart.png)

## <a name="key-concepts"></a>主要概念


**デバイス インターフェイスの GUID とは何ですか。**

カーネル モード ドライバーを初期化、レジスタ、および GUID と呼ばれる公開中に、*デバイス インターフェイスの GUID*します。 通常、アプリでは、公開されている GUID を使用して、関連するドライバーとそのデバイスを検索し、デバイスを識別するハンドルを開きます。 取得されたハンドルは、後続の読み取りおよび書き込み操作に使用されます。

ただし、Winusb.sys の場合、ドライバーの GUID、デバイスのインターフェイスを公開する代わりに提供する 2 つの方法のいずれかで。

-   デバイスの OS の MS 記述子。 デバイスの製造元セット**DeviceInterfaceGUID**デバイスに拡張プロパティ記述子にカスタム プロパティとして。 詳細についてで「拡張プロパティの記述子」のドキュメントを参照してください。 [Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?linkid=617682)します。
-   手動でカスタム INF Winusb.sys をインストールした場合、INF は、INF に GUID を登録します。 参照してください[WinUSB (Winusb.sys) インストール](winusb-installation.md)します。

デバイスの GUID が検出するデバイスのインターフェイス場合、UWP アプリは、そのデバイス インターフェイスの GUID と一致するすべてのデバイスを検索できます。

**Windows での USB デバイス id の表示方法**

すべての USB デバイスが 2 つの情報をいる必要があります: 仕入先 ID と製品 id。

USB の割り当ての場合はこれらの id とデバイスの製造元する必要がありますそれらに公開デバイス。 その情報をどのように入手できますか。

-   読み込まれるデバイス ドライバーがない場合、デバイスの場合でも、Windows が「不明なデバイス」として検出、でも表示できます、識別子のデバイス マネージャーに、**ハードウェア Id**プロパティの値。 その値は、これら 2 つの識別子の組み合わせです。 SuperMUTT デバイスなどの**ハードウェア Id**は"USB\\VID\_045E & PID\_F001"ベンダー id は"0x045E"と、製品 id が"0xF001";。

-   デバイスに対して、INF がある場合からには、その文字列を取得、**モデル**セクション。
-   さまざまなレジストリ設定を検査することができます。 最も簡単な方法を参照してください、

    **HKEY\_ローカル\_マシン\\システム\\ControlSet001\\Enum\\USB\\&lt;ハードウェア id&gt;**

    詳細については、次を参照してください。 [USB デバイスのレジストリ エントリ](usb-device-specific-registry-settings.md)します。

-   アプリ マニフェストによってハードウェア ID を使用して、デバイスを識別します。

    &lt;デバイス Id ="vidpid:045e f001"&gt;

UWP アプリでは、特定の製造元とプロダクト id に一致するすべてのデバイスを検索できます。 デバイス インターフェイスの GUID を指定することで、検索結果を絞り込むことができます。

**USB デバイス クラスとは**

USB によって承認されたデバイス クラス仕様に準拠しているほとんどの USB デバイスの場合。 これらの仕様を使用するのような性質のデバイスは、標準的な方法でそれらの機能を示すことができます。 このアプローチの最大の利点は、デバイスが提供される Microsoft のインボックス クラス ドライバーまたは Winusb.sys の一般的なドライバーを使用できることです。

一部のデバイスが USB に従っていないの場合に指定します。 代わりに、公開*ベンダー定義*機能します。 このようなデバイスの場合、ベンダーは、デバイス ドライバーを提供する必要がありますか、または Winusb.sys ことができます。

このデバイスを記述する必要があります、デバイスがベンダー定義またはデバイス クラスに準拠している、かどうかクラスの関連情報。

-   クラス コード:デバイスが所属するデバイス クラスを示します。
-   サブクラス コード:デバイスのクラス内でデバイスのサブクラスを示します。
-   プロトコルのコード:デバイスを使用するプロトコル。

たとえば、SuperMUTT デバイスは、ベンダー定義されているデバイスと、FF は、情報は、クラスのコードによって示されます。 デバイスは、FEh、02 の h としてサブクラス コードおよびプロトコル コード 00 h としてクラスのコードを示している場合、デバイスが準拠クラス IrDA ブリッジ デバイスであるかを判断できます。
UWP アプリは、これらのデバイス クラスに属しているデバイスと通信できます。

-   ActiveSync
-   CdcControl
-   DeviceFirmwareUpdate
-   IrDA
-   測定
-   PalmSync
-   PersonalHealthcare
-   運動能力
-   ベンダー固有

UWP アプリでは、クラス、サブクラスでは、およびプロトコルのコードの特定のセットと一致するすべてのデバイスを検索できます。

## <a name="get-the-advanced-query-syntax-aqs-string-for-the-device"></a>デバイスの高度なクエリ構文 (AQS) 文字列を取得します。


検出するために使用するデバイスの識別情報を含む高度なクエリ文字列 (AQS) を生成します。 ベンダーと製品 Id、デバイス インターフェイスの GUID を指定することで、またはデバイス クラスでは、文字列を生成できます。

-   ベンダー ID/製品 ID またはデバイス インターフェイスの GUID を指定する場合のオーバー ロードを呼び出す[ **GetDeviceSelector**](https://msdn.microsoft.com/library/windows/apps/dn264022)します。

    SuperMUTT デバイスの例では[ **GetDeviceSelector** ](https://msdn.microsoft.com/library/windows/apps/dn264022)この文字列に類似した AQS 文字列を取得します。

    `"System.Devices.InterfaceClassGuid:="{DEE824EF-729B-4A0E-9C14-B7117D33A817}" AND System.Devices.InterfaceEnabled:=System.StructuredQueryType.Boolean#True AND System.DeviceInterface.WinUsb.UsbVendorId:=1118 AND System.DeviceInterface.WinUsb.UsbProductId:=61441"`

    **注**  デバイス インターフェイス、文字列に表示される GUID がない 1 つの指定したことを確認します。 この GUID は、実際のデバイス インターフェイス UWP アプリの Winusb.sys によって登録された GUID です。

     

-   デバイスまたはそのクラス、サブクラスでは、およびプロトコルのコードのデバイス クラスがわかっている場合は、呼び出す[ **GetDeviceClassSelector** ](https://msdn.microsoft.com/library/windows/apps/dn264013) AQS 文字列を生成します。

    作成、 [ **UsbDeviceClass** ](https://msdn.microsoft.com/library/windows/apps/dn263894)オブジェクトを指定して[ **ClassCode**](https://msdn.microsoft.com/library/windows/apps/dn263948)、 [ **SubclassCode**](https://msdn.microsoft.com/library/windows/apps/dn263956)、および[ **ProtocolCode** ](https://msdn.microsoft.com/library/windows/apps/dn263951)プロパティの値。 または、デバイスのデバイス クラスがわかっている場合は、コンス トラクターを呼び出す特定を指定することによって[ **UsbDeviceClasses** ](https://msdn.microsoft.com/library/windows/apps/dn263904)プロパティ。

## <a name="finding-the-devicethe-basic-way"></a>デバイスの検索-基本的な方法


これは、USB デバイスを検索する最も簡単な方法です。 詳細については、次を参照してください。[クイック スタート: デバイスを使用する一般的な列挙](https://msdn.microsoft.com/library/windows/apps/xaml/hh872189)します。

1.  取得した AQS 文字列を渡す[ **FindAllAsync**](https://msdn.microsoft.com/library/windows/apps/br225432)します。 呼び出しを取得、 [ **DeviceInformationCollection** ](https://msdn.microsoft.com/library/windows/apps/br225395)オブジェクト。
2.  コレクションをループします。 各イテレーションの取得、 [ **DeviceInformation** ](https://msdn.microsoft.com/library/windows/apps/br225393)オブジェクト。
3.  取得、 [ **DeviceInformation.Id** ](https://msdn.microsoft.com/library/windows/apps/br225437)プロパティの値。 文字列値は、デバイスのインスタンス パスです。 たとえば、"\\\\\\\\?\\\\USB\#VID\_045E & PID\_078F\#6 & 1b8ff026 & 0 & 5\#{dee824ef-729b-4a0e-9c14-b7117d33a817}"。
4.  呼び出す[ **FromIdAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264010)デバイス インスタンスの文字列と取得を渡すことによって、 [ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクト。 使用することができますし、 **UsbDevice**コントロール転送の送信などの他の操作を実行するオブジェクト。 アプリがいつ終了したを使用して、 **UsbDevice**オブジェクト、アプリを呼び出すことによって解放する必要があります[**閉じる**](https://msdn.microsoft.com/library/windows/apps/dn263990)します。
    **注**  と UWP アプリの中断、デバイスが自動的に閉じられます。 古いハンドルを使用して、今後の操作を避けるため、アプリをリリースする必要があります、 [ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)参照。

     

```CSharp
    private async void OpenDevice()
    {
        UInt32 vid = 0x045E;
        UInt32 pid = 0x0611;

        string aqs = UsbDevice.GetDeviceSelector(vid, pid);

        var myDevices = await Windows.Devices.Enumeration.DeviceInformation.FindAllAsync(aqs);

        try
        {
            usbDevice = await UsbDevice.FromIdAsync(myDevices[0].Id);
        }
        catch (Exception exception)
        {
            ShowStatus(exception.Message.ToString());
        }
        finally        
        {
            ShowStatus("Opened device for communication.");
        }

    }
```

## <a name="find-the-deviceusing-devicewatcher"></a>デバイスの検出-DeviceWatcher を使用します。


デバイスを動的に列挙することができます。 次に、アプリは、デバイスが追加または削除される場合、またはデバイスのプロパティを変更する場合、通知を受信できます。 詳細については、次を参照してください。[デバイスを追加する場合に通知を取得する方法は、削除、または変更](https://msdn.microsoft.com/library/windows/apps/xaml/hh967756)します。

A [ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)オブジェクトが動的にデバイスを検出するように、追加、システムから削除するアプリを使用できます。

1.  作成、 [ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)デバイスが追加またはシステムから削除されるタイミングを検出するオブジェクト。 呼び出すことによって、オブジェクトを作成する必要があります[ **CreateWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225427) AQS 文字列を指定するとします。
2.  実装し、ハンドラーを登録[ **Added** ](https://msdn.microsoft.com/library/windows/apps/br225450)と[**から削除された**](https://msdn.microsoft.com/library/windows/apps/br225453)上のイベント、 [ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)オブジェクト。 これらのイベント ハンドラーは、(同じ id 情報) を持つデバイスを追加またはシステムから削除されたときに呼び出されます。
3.  開始し、停止、 [ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)オブジェクト。

    アプリを起動する必要があります、 [ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)オブジェクトを呼び出すことによって[**開始**](https://msdn.microsoft.com/library/windows/apps/br225454)追加されたデバイスの検出を開始するため、またはシステムから削除します。 逆に、アプリが停止する必要があります、 **DeviceWatcher**呼び出して[**停止**](https://msdn.microsoft.com/library/windows/apps/br225456)デバイスを検出するために必要でなくなったとき。 このサンプルでは、ユーザーを開始および停止できる 2 つのボタン**DeviceWatcher**します。

このコード例は、作成し、検索するデバイスの監視を開始する方法を示しています。 SuperMUTT デバイスのインスタンス。

```CSharp
void CreateSuperMuttDeviceWatcher(void)
{
    UInt32 vid = 0x045E;
    UInt32 pid = 0x0611;

    string aqs = UsbDevice.GetDeviceSelector(vid, pid);  
    
    var superMuttWatcher = DeviceInformation.CreateWatcher(aqs);
  
    superMuttWatcher.Added += new TypedEventHandler<DeviceWatcher, DeviceInformation>
                              (this.OnDeviceAdded);

    superMuttWatcher.Removed += new TypedEventHandler<DeviceWatcher, DeviceInformationUpdate>
                            (this.OnDeviceRemoved);

    superMuttWatcher.Start();
 }
```

## <a name="open-the-device"></a>デバイスを開く


デバイスを開くには、アプリは、静的メソッドを呼び出して非同期操作を開始する必要があります[ **FromIdAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264010)デバイス インスタンスのパスを渡すと (から取得した[ **DeviceInformation.Id**](https://msdn.microsoft.com/library/windows/apps/br225437))。 その操作の結果を取得することは、 [ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクトで、デバイスが、データ転送の実行などの将来の通信に使用します。

完了した後を使用して、 [ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクト、それを解放する必要があります。 オブジェクトを解放することによって、すべての保留中のデータ転送が取り消されました。 これらの操作の完了コールバック ルーチンは取り消されたエラーまたは完了した操作でも呼び出されます。

C++ アプリを使用して参照を解放する必要があります、**削除**キーワード。 C#または VB のアプリを呼び出す必要があります、 [ **UsbDevice.Dispose** ](https://msdn.microsoft.com/library/windows/apps/dn264007)メソッド。 JavaScript アプリを呼び出す必要があります[ **UsbDevice.Close**](https://msdn.microsoft.com/library/windows/apps/dn263990)します。

[ **FromIdAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264010)失敗する場合は、デバイスが使用するかが見つかりません。

 

 





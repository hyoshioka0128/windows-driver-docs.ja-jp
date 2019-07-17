---
Description: C と C++ WinUSB テンプレートを使用、USB デバイスと通信する Windows デスクトップ アプリを作成する最も簡単な方法です。
title: WinUSB テンプレートに基づいて Windows デスクトップ アプリを記述する
ms.date: 07/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 881c47a571a8a03ee1bf6b6418c7bf69c39db68f
ms.sourcegitcommit: ef6d15e2f4a8ce75a0ee726432574f2e25f061eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2019
ms.locfileid: "68293241"
---
# <a name="write-a-windows-desktop-app-based-on-the-winusb-template"></a>WinUSB テンプレートに基づいて Windows デスクトップ アプリを記述する


**重要な API**

-   [SetupAPI 関数](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)
-   [WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)

C と C++ WinUSB テンプレートを使用、USB デバイスと通信する Windows デスクトップ アプリを作成する最も簡単な方法です。 このテンプレートでは、Windows Driver Kit (WDK) (デバッグ ツールの Windows) で、Microsoft Visual Studio (Professional または Ultimate) との統合環境が必要です。 開始点としては、テンプレートを使用することができます。

## <a name="prerequisites"></a>必須コンポーネント


-   統合開発環境を設定するには、Microsoft Visual Studio Ultimate 2019 または Microsoft Visual Studio Professional 2019 最初にインストールし、WDK をインストールし。 Visual Studio と WDK の入手方法について詳しくは、[こちら](https://go.microsoft.com/fwlink/p/?linkid=239721)をご覧ください。
-   WDK をインストールするときに、Windows 用デバッグ ツールが含まれます。 詳細については、次を参照してください。[ダウンロードとデバッグ ツールの Windows にインストール](https://go.microsoft.com/fwlink/p/?linkid=235427)します。

## <a name="creating-a-winusb-application"></a>WinUSB アプリケーションを作成します。

テンプレートからアプリケーションの作成。

1.  **新しいプロジェクト**ダイアログ ボックスで、型、上部にある検索ボックスに**USB です。**
2.  中央のペインで選択**WinUSB アプリケーション (ユニバーサル)** します。
3.  **[次へ]** をクリックします。
4.  プロジェクト名を入力、保存を選択する場所、およびクリック**作成**です。

    次のスクリーン ショットに示す、**新しいプロジェクト**の ダイアログ ボックス、 **WinUSB アプリケーション (ユニバーサル)** テンプレート。

    ![winusb テンプレートの新しいプロジェクトの作成最初 画面](images/winusb-template-creation-1.png)

    ![winusb テンプレートの新しいプロジェクトの作成 2 番目 画面](images/winusb-template-creation-2.png)

    このトピックでは、Visual Studio プロジェクトの名前がある前提としています。 *USB Application1*します。

    Visual Studio により、1 つのプロジェクトと 1 つのソリューションが作られます。 ソリューション、プロジェクト、および内のプロジェクトに属するファイルを確認できます、**ソリューション エクスプ ローラー**ウィンドウで、次のスクリーン ショットに示すようにします。 ( **[ソリューション エクスプローラー]** ウィンドウが表示されない場合は、 **[表示]** メニューの **[ソリューション エクスプローラー]** を選びます)。ソリューションに含まれる、 C++ USB Application1 という名前のアプリケーション プロジェクト。

    ![winusb テンプレート ソリューション エクスプ ローラー 1](images/winusb-template-solution-explorer-1.png)

    USB Application1 プロジェクトには、アプリケーションのソース ファイルが含まれます。 アプリケーション ソース コードを確認する場合は、下に表示されるファイルのいずれかを開くことができます**ソースファイル**します。  
    
5. ドライバー パッケージのプロジェクトをソリューションに追加します。 (ソリューション ' USB Application1') のソリューションを右クリックし、をクリックして**追加** \> **新しいプロジェクト**次のスクリーン ショットに示すようにします。

    ![winusb テンプレートの作成 2 番目プロジェクト追加](images/winusb-template-creation-3.png)

6. **新しいプロジェクト**ダイアログ ボックスで、上部にある検索ボックスをもう一度入力**USB です。**
7.  中央のペインで選択**WinUSB INF ドライバー パッケージ**します。
8.  **[次へ]** をクリックします。
9.  プロジェクト名を入力し、クリックして**作成**です。

    次のスクリーン ショットに示す、**新しいプロジェクト**の ダイアログ ボックス、 **WinUSB INF ドライバー パッケージ**テンプレート。

    ![winusb テンプレートの 2 つ目プロジェクト作成最初 画面](images/winusb-template-creation-4.png)

    ![winusb テンプレート 2 プロジェクトの作成 2 番目の画面](images/winusb-template-creation-5.png)

    このトピックでは、Visual Studio プロジェクトの名前がある前提としています。 *USB Application1 パッケージ*します。        

    USB Application1 パッケージ プロジェクトには、デバイス ドライバーとして Microsoft が提供 Winusb.sys ドライバーをインストールするために使用される INF ファイルが含まれています。

    **ソリューション エクスプ ローラー**の次のスクリーン ショットに示すようになりました、両方のプロジェクトを含める必要があります。

    ![winusb テンプレート ソリューション エクスプ ローラー 2](images/winusb-template-solution-explorer-2.png)

10.  USBApplication1.inf、INF ファイルでは、これらの行を見つけます。

    `%DeviceName% =USB_Install, USB\VID_vvvv&PID_pppp`

11.  VID を置き換える\_vvvv & PID\_pppp デバイスのハードウェア ID を使用します。 デバイス マネージャーから、ハードウェア ID を取得します。 デバイス マネージャーでは、デバイスのプロパティを表示します。 **詳細** タブで、表示、**ハードウェア Id**プロパティの値。
12.  **ソリューション エクスプ ローラー**ウィンドウで、右クリック**ソリューション ' USB Application1' (2/2 プロジェクト)** 、選択**Configuration Manager**します。 構成と、アプリケーション プロジェクトとパッケージのプロジェクトの両方のプラットフォームを選択します。 この演習で選択デバッグおよび x64 では、次のスクリーン ショットに示すようにします。

![winusb アプリケーション テンプレート](images/winusb-template-configuration-manager.png)

## <a name="building-deploying-and-debugging-the-project"></a>ビルド、配置、およびプロジェクトのデバッグ

これまで、この演習では、プロジェクトを作成するのに Visual Studio を使用しました。 次に、デバイスが接続されているデバイスを構成する必要があります。 テンプレートでは、デバイスのドライバーとして Winusb ドライバーがインストールされていることが必要です。

テストとデバッグ環境を持つことができます。

-   2 つのコンピューターのセットアップ: ホスト コンピューターと対象コンピューター。 開発およびホスト コンピューターで Visual Studio でプロジェクトをビルドするとします。 デバッガーはホスト コンピューター上で実行され、Visual Studio のユーザー インターフェイスで利用できます。 テスト アプリケーションをデバッグすると、ドライバーは、ターゲット コンピューターで実行されます。

-   1 台のコンピューターのセットアップ:1 台のコンピューターで、ターゲットとホストを実行します。 Visual Studio でプロジェクトをビルドを開発し、デバッガーとアプリケーションを実行します。

展開してインストール、読み込むには、するか、および次の手順に従って、アプリケーションとドライバーをデバッグすることができます。

-   **2 つのコンピューターのセットアップ**

    1.  次の手順で、対象のコンピュータをプロビジョニング[ドライバーの展開とテスト用にプロビジョニング](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)します。
        **注:** プロビジョニングすると、WDKRemoteUser という名前のターゲット コンピューターで、ユーザーが作成されます。 プロビジョニングが完了したら、WDKRemoteUser に切り替え、ユーザーが表示されます。 
    2.  ホスト コンピューター上で、Visual Studio でソリューションを開きます。
    3.  Main.cpp では、OpenDevice の呼び出しの前にこの行を追加します。

        `system ("pause")`

        行は、アプリケーションを起動したときに一時停止です。 これは、リモート デバッグで役に立ちます。

    4.  Pch.h には、この行を含めます。

        `#include <cstdlib>`

        ステートメントは、これが必要です、`system()`前の手順で呼び出します。

    5.  **ソリューション エクスプ ローラー** USB Application1 パッケージを右クリックして、ウィンドウ、**プロパティ**します。
    6.  **USB Application1 パッケージのプロパティ ページ**に移動します ウィンドウの左側のウィンドウで、**構成プロパティ&gt;ドライバー インストール&gt;展開**ように、次のスクリーン ショット。
    7.  **[展開前にドライバーの以前のバージョンを削除する]** チェック ボックスをオンにします。
    8.  **[リモート コンピューター名]** については、テストとデバッグ用に構成したコンピューターの名前を選んでください。 この演習では、dbg ターゲットをという名前のコンピューターを使用します。
    9.  選択**インストール/再インストールを確認します**します。 **[適用]** をクリックします。

        ![winusb テンプレートのデプロイ](images/winusb-template-deployment.png)

    10. プロパティ ページに移動します**構成プロパティ&gt;デバッグ**を選択し、**デバッグ ツールの Windows – リモート デバッガー**の次のスクリーン ショットに示すようにします。

        ![winusb テンプレートのリモート デバッガー](images/winusb-template-remote-debugger.png)

    11. 選択**ソリューションのビルド**から、**ビルド**メニュー。 Visual Studio に表示されるビルドの進行状況、**出力**ウィンドウ。 ( **[出力]** ウィンドウが表示されていない場合は、 **[表示]** メニューの **[出力]** をクリックします)。この演習では、x64 用のプロジェクトを作成した Windows 10 を実行しているシステム。
    12. 選択**ソリューションの配置**から、**ビルド**メニュー。 

ターゲット コンピューターで実行されているドライバーのインストール スクリプトが表示されます。 %Systemdrive% に、ドライバー ファイルがコピーされます\\drivertest\\ターゲット コンピューター上のドライバー フォルダー。 .inf、.cat、test cert、.sys など、必要なファイルがすべて %systemdrive%\\drivertest\\drivers フォルダーに存在することを確認します。 デバイスは、エラーなしでデバイス マネージャーを表示する必要があります。

ホスト コンピューターでは、このメッセージが表示されます、**出力**ウィンドウ。

```syntax
Deploying driver files for project 
"<path>\visual studio 14\Projects\USB Application1\USB Application1 Package\USB Application1 Package.vcxproj".  
Deployment may take a few minutes...
========== Build: 1 succeeded, 0 failed, 1 up-to-date, 0 skipped ==========
```

**アプリケーションをデバッグするには**

1.  ホスト コンピューターに移動します。 **x64 &gt; Win8.1Debug**ソリューション フォルダーにします。
2.  対象のコンピュータに UsbApplication1.exe アプリケーションの実行ファイルをコピーします。
3.  ターゲット コンピューターでは、アプリケーションを起動します。
4.  ホスト コンピューターから、**デバッグ**メニューの **プロセスにアタッチ**します。
5.  ウィンドウで、次のように選択します。 **Windows ユーザー モード デバッガー** (デバッグ ツールの Windows)、トランスポートや、ターゲット コンピューターの名前では、この例で dbg のターゲットと修飾子としてこの図のようにします。

    ![winusb テンプレートのデバッグ設定](images/winusb-template6.png)

6.  一覧からアプリケーションを選択**選択可能なプロセス**クリック**アタッチ**。 使用してデバッグできます**イミディ エイト ウィンドウ**でオプションを使用して、または**デバッグ**メニュー。

上記の手順を使用して、アプリケーションをデバッグする**デバッグ ツールの Windows – リモート デバッガー**します。 使用する場合、**リモート Windows デバッガー** (Visual Studio に含まれているデバッガー) し、次の手順に従います。

1.  対象のコンピューターには、ファイアウォール経由で許可されているアプリのリストに msvsmon.exe を追加します。
2.  Visual Studio リモート デバッグ モニターにある c: 起動\\DriverTest\\msvsmon\\msvsmon.exe します。
3.  C: などの作業フォルダーを作成\\remotetemp します。
4.  ターゲット コンピューター上の作業フォルダーに UsbApplication1.exe アプリケーションの実行ファイルをコピーします。
5.  Visual Studio で、ホスト コンピューターでを右クリックし、 **USB Application1 パッケージ**順に選択して、**プロジェクトのアンロード**します。
6.  右クリックし、 **USB Application1**プロジェクトで、プロジェクトのプロパティで、展開、**構成プロパティ**ノードをクリックします**デバッグ**します。
7.  変更**起動するデバッガー**に**リモート Windows デバッガー**します。
8.  記載されている手順に従って、リモート コンピューターで実行可能ファイルを実行するプロジェクト設定を変更[、プロジェクト ビルドのローカルのリモート デバッグ](https://docs.microsoft.com/visualstudio/debugger/remote-debugging?view=vs-2015)します。 確認します**作業ディレクトリ**と**リモート コマンド**プロパティには、ターゲット コンピューターのフォルダーが反映されます。
9.  アプリケーションのデバッグ、**ビルド**メニューの [**デバッグの開始]** 、またはキーを押します**f5 キー。**

-   **1 台のコンピューターのセットアップ:**

    1.  アプリケーションとドライバーのインストール パッケージをビルドするには、選択**ソリューションのビルド**から、**ビルド**メニュー。 Visual Studio に表示されるビルドの進行状況、**出力**ウィンドウ。 ( **[出力]** ウィンドウが表示されていない場合は、 **[表示]** メニューの **[出力]** をクリックします)。この演習では、x64 用のプロジェクトを作成した Windows 10 を実行しているシステム。
    2.  パッケージ化、Windows エクスプ ローラーで、USB Application1 フォルダーに移動しますおよびに移動し、構築されたドライバーを表示する**x64\>デバッグ\>USB Application1 パッケージ**します。 ドライバー パッケージには、いくつかのファイルが含まれています。MyDriver.inf はドライバーをインストールするときに、Windows が使用する情報ファイルで、mydriver.cat はインストーラーを使用してドライバー パッケージのテスト署名を検証するカタログ ファイルです。 これらのファイルは、次のスクリーン ショットに表示されます。

        ![winusb アプリケーション テンプレート](images/winusb-template3.png)

        **注**パッケージに含まれるドライバー ファイルがありません。 INF ファイルは、Windows で検出されたインボックス ドライバー Winusb.sys を参照しているためにである\\System32 フォルダー。
    3.  ドライバーを手動でインストールします。 デバイス マネージャーでは、パッケージに、INF を指定することで、ドライバーを更新します。 前のセクションで示すようにソリューション フォルダーにあるドライバ パッケージ をポイントします。
    4.  右クリックし、 **USB Application1**プロジェクトで、プロジェクトのプロパティで、展開、**構成プロパティ**ノードをクリックします**デバッグ**します。
    5.  変更**起動するデバッガー**に**ローカル Windows デバッガー**します。
    6.  7.  USB Application1 パッケージ プロジェクトを右クリックして**プロジェクトのアンロード**します。
    8.  アプリケーションのデバッグ、**ビルド**メニューの [**デバッグの開始]** 、またはキーを押します**f5 キーを押して**します。

## <a name="template-code-discussion"></a>テンプレート コードの説明


テンプレートは、お客様のデスクトップ アプリケーションの開始点です。 USB Application1 プロジェクトは、ソース ファイル device.cpp と main.cpp にします。

Main.cpp ファイルには、アプリケーションのエントリ ポイントが含まれています。 \_tmain します。 Device.cpp には、デバイスを識別するハンドルを開いたり閉じたりするすべてのヘルパー関数が含まれています。

テンプレートでは、device.h をという名前のヘッダー ファイルもあります。 このファイルには、デバイス インターフェイスの GUID (後述) とデバイスの定義が含まれています。\_情報を格納するデータ構造が、アプリケーションによって取得します。 たとえば、OpenDevice によって取得され、後続の操作で使用される WinUSB インターフェイスのハンドルを格納します。

```cpp
typedef struct _DEVICE_DATA {

    BOOL                    HandlesOpen;
    WINUSB_INTERFACE_HANDLE WinusbHandle;
    HANDLE                  DeviceHandle;
    TCHAR                   DevicePath[MAX_PATH];

} DEVICE_DATA, *PDEVICE_DATA;
```

### <a href="" id="deviceinstance"></a>インスタンス パスを取得する - デバイスの device.cpp で RetrieveDevicePath を参照してください。

USB デバイスへのアクセス、アプリケーションでは、呼び出すことによって、デバイスの有効なファイル ハンドルを作成**CreateFile**します。 その呼び出しでは、アプリケーションがデバイス パスのインスタンスを取得する必要があります。 アプリでは、デバイス パスを取得する[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)ルーチンを Winusb.sys のインストールに使用された INF ファイルで、デバイス インターフェイスの GUID を指定します。 GUID を名前付き GUID 定数を宣言する Device.h\_DEVINTERFACE\_USBApplication1 します。 これらのルーチンを使用するは、アプリケーションは、指定したデバイスのインターフェイス クラスのすべてのデバイスを列挙し、デバイスのデバイス パスを取得します。

```cpp
HRESULT
RetrieveDevicePath(
    _Out_bytecap_(BufLen) LPTSTR DevicePath,
    _In_                  ULONG  BufLen,
    _Out_opt_             PBOOL  FailureDeviceNotFound
    )
/*++

Routine description:

    Retrieve the device path that can be used to open the WinUSB-based device.

    If multiple devices have the same device interface GUID, there is no
    guarantee of which one will be returned.

Arguments:

    DevicePath - On successful return, the path of the device (use with CreateFile).

    BufLen - The size of DevicePath's buffer, in bytes

    FailureDeviceNotFound - TRUE when failure is returned due to no devices
        found with the correct device interface (device not connected, driver
        not installed, or device is disabled in Device Manager); FALSE
        otherwise.

Return value:

    HRESULT

--*/
{
    BOOL                             bResult = FALSE;
    HDEVINFO                         deviceInfo;
    SP_DEVICE_INTERFACE_DATA         interfaceData;
    PSP_DEVICE_INTERFACE_DETAIL_DATA detailData = NULL;
    ULONG                            length;
    ULONG                            requiredLength=0;
    HRESULT                          hr;

    if (NULL != FailureDeviceNotFound) {

        *FailureDeviceNotFound = FALSE;
    }

    //
    // Enumerate all devices exposing the interface
    //
    deviceInfo = SetupDiGetClassDevs(&GUID_DEVINTERFACE_USBApplication1,
                                     NULL,
                                     NULL,
                                     DIGCF_PRESENT | DIGCF_DEVICEINTERFACE);

    if (deviceInfo == INVALID_HANDLE_VALUE) {

        hr = HRESULT_FROM_WIN32(GetLastError());
        return hr;
    }

    interfaceData.cbSize = sizeof(SP_DEVICE_INTERFACE_DATA);

    //
    // Get the first interface (index 0) in the result set
    //
    bResult = SetupDiEnumDeviceInterfaces(deviceInfo,
                                          NULL,
                                          &GUID_DEVINTERFACE_USBApplication1,
                                          0,
                                          &interfaceData);

    if (FALSE == bResult) {

        //
        // We would see this error if no devices were found
        //
        if (ERROR_NO_MORE_ITEMS == GetLastError() &&
            NULL != FailureDeviceNotFound) {

            *FailureDeviceNotFound = TRUE;
        }

        hr = HRESULT_FROM_WIN32(GetLastError());
        SetupDiDestroyDeviceInfoList(deviceInfo);
        return hr;
    }

    //
    // Get the size of the path string
    // We expect to get a failure with insufficient buffer
    //
    bResult = SetupDiGetDeviceInterfaceDetail(deviceInfo,
                                              &interfaceData,
                                              NULL,
                                              0,
                                              &requiredLength,
                                              NULL);

    if (FALSE == bResult && ERROR_INSUFFICIENT_BUFFER != GetLastError()) {

        hr = HRESULT_FROM_WIN32(GetLastError());
        SetupDiDestroyDeviceInfoList(deviceInfo);
        return hr;
    }

    //
    // Allocate temporary space for SetupDi structure
    //
    detailData = (PSP_DEVICE_INTERFACE_DETAIL_DATA)
        LocalAlloc(LMEM_FIXED, requiredLength);

    if (NULL == detailData)
    {
        hr = E_OUTOFMEMORY;
        SetupDiDestroyDeviceInfoList(deviceInfo);
        return hr;
    }

    detailData->cbSize = sizeof(SP_DEVICE_INTERFACE_DETAIL_DATA);
    length = requiredLength;

    //
    // Get the interface's path string
    //
    bResult = SetupDiGetDeviceInterfaceDetail(deviceInfo,
                                              &interfaceData,
                                              detailData,
                                              length,
                                              &requiredLength,
                                              NULL);

    if(FALSE == bResult)
    {
        hr = HRESULT_FROM_WIN32(GetLastError());
        LocalFree(detailData);
        SetupDiDestroyDeviceInfoList(deviceInfo);
        return hr;
    }

    //
    // Give path to the caller. SetupDiGetDeviceInterfaceDetail ensured
    // DevicePath is NULL-terminated.
    //
    hr = StringCbCopy(DevicePath,
                      BufLen,
                      detailData->DevicePath);

    LocalFree(detailData);
    SetupDiDestroyDeviceInfoList(deviceInfo);

    return hr;
}
```

前の関数では、アプリケーションは、これらのルーチンを呼び出すことによって、デバイス パスを取得します。

1.  [**SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)を識別するハンドルを取得する、*デバイス情報設定されている*、指定したデバイスのインターフェイス クラス GUIDに一致するすべてのインストールされているデバイスに関する情報を格納する配列\_DEVINTERFACE\_USBApplication1 します。 配列内の各要素と呼ばれる、*デバイス インターフェイス*がインストールされ、システムに登録されているデバイスに対応しています。 デバイスのインターフェイス クラスは、デバイス インターフェイス INF ファイルで定義した GUID を渡すことによって識別されます。 関数は、デバイス情報のセットに HDEVINFO ハンドルを返します。
2.  [**SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)デバイスを列挙するインターフェイスでデバイス情報設定し、デバイス インターフェイスに関する情報を取得します。

    この呼び出しでは、次のものが必要です。

    -   初期化された呼び出し元が割り当てた[ **SP\_デバイス\_インターフェイス\_データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)構造を持つその**cbSize**メンバーに設定構造体のサイズ。
    -   手順 1 から HDEVINFO ハンドル。
    -   デバイスのインターフェイスの INF ファイルで定義した GUID です。

    [**SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)デバイス インターフェイスの指定したインデックスのデバイス情報設定の配列を検索し、初期化された入力[ **SP\_デバイス\_インターフェイス\_データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)インターフェイスに関する基本的なデータを含む構造体。

    **注**デバイス情報のセット内のすべてのデバイス インターフェイスを列挙するために呼び出す[ **SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)関数が戻るまでループで**FALSE**障害のエラー コードはエラーと\_いいえ\_詳細\_項目。 エラー\_いいえ\_詳細\_項目のエラー コードを呼び出すことによって取得できる**GetLastError**します。 反復処理ごとに、メンバーのインデックスをインクリメントします。

    または、呼び出せる[ **SetupDiEnumDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)するデバイス情報のセットを列挙し、呼び出し元が割り当てた内でのインデックスで指定された、デバイスのインターフェイス要素に関する情報を返します[ **SP\_DEVINFO\_データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)構造体。 この構造体への参照を渡すことができますし、 *DeviceInfoData*のパラメーター、 [ **SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)関数。

3.  [**SetupDiGetDeviceInterfaceDetail** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)デバイス インターフェイスの詳細なデータを取得します。 情報が返されます、 [ **SP\_デバイス\_インターフェイス\_詳細\_データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_detail_data_a)構造体。 のサイズ、 **SP\_デバイス\_インターフェイス\_詳細\_データ**構造の変化に合わせて、 **SetupDiGetDeviceInterfaceDetail**が呼び出されます2 回クリックします。 最初の呼び出しが用に割り当てるバッファーのサイズを取得、 **SP\_デバイス\_インターフェイス\_詳細\_データ**構造体。 2 番目の呼び出しでは、インターフェイスに関する詳しい情報を割り当てられたバッファーを設定します。
    1.  呼び出し[ **SetupDiGetDeviceInterfaceDetail** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)で*DeviceInterfaceDetailData*パラメーターに設定**NULL**します。 関数が適切なバッファー サイズを返します、 *requiredlength*パラメーター。 この呼び出しがエラーで失敗\_不十分\_バッファーのエラー コード。 このエラー コードが必要です。
    2.  メモリを割り当て、 [ **SP\_デバイス\_インターフェイス\_詳細\_データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_detail_data_a)構造が取得される適切なバッファー サイズに基づいて、*requiredlength*パラメーター。
    3.  呼び出し[ **SetupDiGetDeviceInterfaceDetail** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)もう一度で初期化された構造体への参照を渡すと、 *DeviceInterfaceDetailData*パラメーター。 関数から制御が戻るときに、構造体はインターフェイスに関する詳しい情報を入力されます。 デバイスのパスが、 [ **SP\_デバイス\_インターフェイス\_詳細\_データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_detail_data_a)構造体の**DevicePath**メンバー。

### <a href="" id="filehandle"></a>ファイルを作成するデバイスの処理 - device.cpp OpenDevice を参照してください。

デバイスを対話のニーズ、WinUSB インターフェイス デバイス上の最初の (既定値) インターフェイスへのハンドル。 テンプレート コードがファイル ハンドルと WinUSB インターフェイスのハンドルを取得し、デバイスに格納\_データ構造体。

```cpp
HRESULT
OpenDevice(
    _Out_     PDEVICE_DATA DeviceData,
    _Out_opt_ PBOOL        FailureDeviceNotFound
    )
/*++

Routine description:

    Open all needed handles to interact with the device.

    If the device has multiple USB interfaces, this function grants access to
    only the first interface.

    If multiple devices have the same device interface GUID, there is no
    guarantee of which one will be returned.

Arguments:

    DeviceData - Struct filled in by this function. The caller should use the
        WinusbHandle to interact with the device, and must pass the struct to
        CloseDevice when finished.

    FailureDeviceNotFound - TRUE when failure is returned due to no devices
        found with the correct device interface (device not connected, driver
        not installed, or device is disabled in Device Manager); FALSE
        otherwise.

Return value:

    HRESULT

--*/
{
    HRESULT hr = S_OK;
    BOOL    bResult;

    DeviceData->HandlesOpen = FALSE;

    hr = RetrieveDevicePath(DeviceData->DevicePath,
                            sizeof(DeviceData->DevicePath),
                            FailureDeviceNotFound);

    if (FAILED(hr)) {

        return hr;
    }

    DeviceData->DeviceHandle = CreateFile(DeviceData->DevicePath,
                                          GENERIC_WRITE | GENERIC_READ,
                                          FILE_SHARE_WRITE | FILE_SHARE_READ,
                                          NULL,
                                          OPEN_EXISTING,
                                          FILE_ATTRIBUTE_NORMAL | FILE_FLAG_OVERLAPPED,
                                          NULL);

    if (INVALID_HANDLE_VALUE == DeviceData->DeviceHandle) {

        hr = HRESULT_FROM_WIN32(GetLastError());
        return hr;
    }

    bResult = WinUsb_Initialize(DeviceData->DeviceHandle,
                                &DeviceData->WinusbHandle);

    if (FALSE == bResult) {

        hr = HRESULT_FROM_WIN32(GetLastError());
        CloseHandle(DeviceData->DeviceHandle);
        return hr;
    }

    DeviceData->HandlesOpen = TRUE;
    return hr;
}
```

1.  アプリによる呼び出し**CreateFile**先ほど取得したデバイスのパスを指定することで、デバイスのファイル ハンドルを作成します。 ファイルを使用して\_フラグ\_OVERLAPPED WinUSB がこの設定に依存するためのフラグします。
2.  ファイル ハンドルを使用すると、デバイス、アプリは WinUSB インターフェイスのハンドルを作成します。 [WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)ファイル ハンドルが、代わりに、ターゲット デバイスを識別するために、このハンドルを使用します。 WinUSB インターフェイス ハンドルをアプリの呼び出しを取得する[ **WinUsb\_初期化**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)ファイル ハンドルを渡すことによって。 I/O 要求をデバイスに送信して、デバイスから情報を取得、後続の呼び出しで受信したハンドルを使用します。

### <a name="release-the-device-handles---see-closedevice-in-devicecpp"></a>デバイス ハンドルのリリース - device.cpp CloseDevice を参照してください。

テンプレート コードでは、ファイル ハンドルとデバイスの WinUSB インターフェイスのハンドルを解放するコードを実装します。

-   **CloseHandle**によって作成されたハンドルを解放する**CreateFile**」の説明に従って、[ファイル ハンドルを作成、デバイスの](#filehandle)このチュートリアルの「します。
-   [**WinUsb\_Free** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)によって返されると、デバイスの WinUSB インターフェイスのハンドルを解放する[ **WinUsb\_初期化**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)します。

```cpp
VOID
CloseDevice(
    _Inout_ PDEVICE_DATA DeviceData
    )
/*++

Routine description:

    Perform required cleanup when the device is no longer needed.

    If OpenDevice failed, do nothing.

Arguments:

    DeviceData - Struct filled in by OpenDevice

Return value:

    None

--*/
{
    if (FALSE == DeviceData->HandlesOpen) {

        //
        // Called on an uninitialized DeviceData
        //
        return;
    }

    WinUsb_Free(DeviceData->WinusbHandle);
    CloseHandle(DeviceData->DeviceHandle);
    DeviceData->HandlesOpen = FALSE;

    return;
}
```

## <a name="next-steps"></a>次の手順


次に、デバイス情報を取得するを送信し、デバイスにデータ転送にこれらのトピックを参照してください。

-   [WinUSB 関数を使用して USB デバイスへのアクセスします。](using-winusb-api-to-communicate-with-a-usb-device.md)

    デバイスの速度、インターフェイスの記述子、関連するエンドポイント、およびそのパイプなどの USB に固有の情報については、デバイスを照会する方法について説明します。

-   [WinUSB デスクトップ アプリから USB アイソクロナス転送を送信します。](getting-set-up-to-use-windows-devices-usb.md)

    USB デバイスのアイソクロナス エンドポイント間でデータを転送します。

## <a name="related-topics"></a>関連トピック
[USB デバイスの Windows デスクトップ アプリ](windows-desktop-app-for-a-usb-device.md)  
[ドライバーの展開およびテスト用のコンピューターをプロビジョニングします。](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)  




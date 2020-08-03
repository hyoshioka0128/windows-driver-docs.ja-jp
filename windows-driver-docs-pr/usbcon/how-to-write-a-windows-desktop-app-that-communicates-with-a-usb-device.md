---
Description: USB デバイスと通信する Windows デスクトップアプリを作成する最も簡単な方法は、C/c + + WinUSB テンプレートを使用することです。
title: WinUSB テンプレートに基づいて Windows デスクトップ アプリを記述する
ms.date: 07/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 04049fa103cd92251c84c52408f06e74c5f81260
ms.sourcegitcommit: e2d27f19033482dece6350f3190ce073b1cd9f06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87479134"
---
# <a name="write-a-windows-desktop-app-based-on-the-winusb-template"></a>WinUSB テンプレートに基づいて Windows デスクトップ アプリを記述する

USB デバイスと通信する Windows デスクトップアプリを作成する最も簡単な方法は、C/c + + WinUSB テンプレートを使用することです。 このテンプレートには、Windows Driver Kit (WDK) と Microsoft Visual Studio (Professional または Ultimate) を備えた統合環境が必要です。 このテンプレートは、開始点として使用できます。

## <a name="prerequisites"></a>[前提条件]

- 統合開発環境をセットアップするには、最初に Microsoft Visual Studio Ultimate 2019 または Microsoft Visual Studio Professional 2019 をインストールし、次に WDK をインストールします。 Visual Studio と WDK のセットアップ方法については、「 [wdk のダウンロード」ページ](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)を参照してください。
- Windows 用デバッグツールは、WDK をインストールするときに含まれています。 詳細については、「 [Windows 用デバッグツールのダウンロードとインストール](https://go.microsoft.com/fwlink/p/?linkid=235427)」を参照してください。

## <a name="creating-a-winusb-application"></a>WinUSB アプリケーションの作成

テンプレートからアプリケーションを作成するには、次のようにします。

1. [**新しいプロジェクト**] ダイアログボックスの上部にある [検索] ボックスに、「USB」と入力し**ます。**
2. 中央のウィンドウで、[ **Winusb アプリケーション (Universal)**] を選択します。
3. **[次へ]** をクリックします。
4. プロジェクト名を入力し、保存場所を選択して、[**作成**] をクリックします。

    次のスクリーンショットは、 **Winusb アプリケーション (ユニバーサル)** テンプレートの [**新しいプロジェクト**] ダイアログボックスを示しています。

    ![winusb テンプレートの新しいプロジェクト作成の最初の画面](images/winusb-template-creation-1.png)

    ![winusb テンプレートの新しいプロジェクト作成2番目の画面](images/winusb-template-creation-2.png)

    このトピックでは、Visual Studio プロジェクトの名前が*USB アプリケーション 1*であることを前提としています。

    Visual Studio により、1 つのプロジェクトと 1 つのソリューションが作られます。 次のスクリーンショットに示すように、[**ソリューションエクスプローラー** ] ウィンドウで、プロジェクトに属しているソリューション、プロジェクト、およびファイルを確認できます。 (**ソリューションエクスプローラー**ウィンドウが表示されていない場合は、[**表示**] メニューの [**ソリューションエクスプローラー** ] をクリックします)。このソリューションには、USB アプリケーション1という名前の C++ アプリケーションプロジェクトが含まれています。

    ![winusb テンプレートソリューションエクスプローラー1](images/winusb-template-solution-explorer-1.png)

    USB アプリケーション1プロジェクトには、アプリケーションのソースファイルが含まれています。 アプリケーションのソースコードを確認する場合は、[**ソースファイル**] の下に表示される任意のファイルを開くことができます。  

5. ソリューションにドライバーパッケージプロジェクトを追加します。 ソリューション ("USB アプリケーション 1") を右クリックし、 **Add** \> 次のスクリーンショットに示すように、[**新しいプロジェクト**の追加] をクリックします。

    ![winusb テンプレート作成の2番目のプロジェクトの追加](images/winusb-template-creation-3.png)

6. [**新しいプロジェクト**] ダイアログボックスの上部にある [検索] ボックスに、もう一度「USB」と入力し**ます。**
7. 中央のウィンドウで、[ **Winusb INF Driver Package**] を選択します。
8. **[次へ]** をクリックします。
9. プロジェクト名を入力し、[**作成**] をクリックします。

    次のスクリーンショットは、 **Winusb INF ドライバーパッケージ**テンプレートの [**新しいプロジェクト**] ダイアログボックスを示しています。

    ![winusb テンプレート2番目のプロジェクト作成の最初の画面](images/winusb-template-creation-4.png)

    ![winusb テンプレート2番目のプロジェクト作成2画面](images/winusb-template-creation-5.png)

    このトピックでは、Visual Studio プロジェクトの名前が*USB アプリケーション 1 Package*であることを前提としています。

    USB アプリケーション1パッケージプロジェクトには、デバイスドライバーとして Microsoft が提供する Winusb.sys ドライバーをインストールするために使用される INF ファイルが含まれています。

    次のスクリーンショットに示すように、**ソリューションエクスプローラー**に両方のプロジェクトを含める必要があります。

    ![winusb テンプレートソリューションエクスプローラー2](images/winusb-template-solution-explorer-2.png)

10. INF ファイルの USBApplication1 で、次のコードを見つけます。`%DeviceName% =USB_Install, USB\VID_vvvv&PID_pppp`

11. VID \_ vvvv&PID \_ pppp を、使用しているデバイスのハードウェア ID に置き換えます。 デバイスマネージャーからハードウェア ID を取得します。 デバイスマネージャーで、デバイスのプロパティを表示します。 [**詳細**] タブで、"**ハードウェア id** " プロパティの値を確認します。
12. [**ソリューションエクスプローラー** ] ウィンドウで、[ **Solution ' USB アプリケーション 1 ' (2 of 2 projects)**] を右クリックし、[ **Configuration Manager**] を選択します。 アプリケーションプロジェクトとパッケージプロジェクトの両方の構成とプラットフォームを選択します。 この演習では、次のスクリーンショットに示すように、[デバッグ] と [x64] を選択します。

![winusb アプリケーションテンプレート](images/winusb-template-configuration-manager.png)

## <a name="building-deploying-and-debugging-the-project"></a>プロジェクトのビルド、配置、およびデバッグ

この演習では、Visual Studio を使用してプロジェクトを作成しました。 次に、デバイスが接続されるデバイスを構成する必要があります。 このテンプレートを使用するには、Winusb ドライバーがデバイスのドライバーとしてインストールされている必要があります。

テストおよびデバッグ環境では、次のことが可能です。

- 2台のコンピューターのセットアップ: ホストコンピューターとターゲットコンピューター。 ホストコンピューター上の Visual Studio でプロジェクトを開発し、ビルドします。 デバッガーはホスト コンピューター上で実行され、Visual Studio のユーザー インターフェイスで利用できます。 アプリケーションをテストしてデバッグすると、ドライバーはターゲットコンピューターで実行されます。

- 単一コンピューターのセットアップ: ターゲットとホストが1台のコンピューター上で実行されます。 Visual Studio でプロジェクトを開発してビルドし、デバッガーとアプリケーションを実行します。

次の手順に従って、アプリケーションとドライバーをデプロイ、インストール、読み込み、デバッグできます。

- **2台のコンピューターのセットアップ**

  1. 「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の手順に従って、対象のコンピューターをプロビジョニングします。
        **注:** プロビジョニングによって、WDKRemoteUser という名前のターゲットコンピューターにユーザーが作成されます。 プロビジョニングが完了すると、ユーザーが WDKRemoteUser に切り替えられることがわかります。
  2. ホスト コンピューター上で、Visual Studio でソリューションを開きます。
  3. メイン .cpp で、OpenDevice 呼び出しの前に次の行を追加します。

  ```syntax
  system ("pause")
  ```

  この行により、起動時にアプリケーションが一時停止します。 これは、リモートデバッグに役立ちます。
  
  4. .Pch で、次の行を追加します。

  ```syntax
  #include <cstdlib>
  ```

  このインクルードステートメントは、前の `system()` 手順での呼び出しに必要です。

  5. [**ソリューションエクスプローラー** ] ウィンドウで、[USB アプリケーション 1 Package] を右クリックし、[**プロパティ**] を選択します。
  6. 次のスクリーンショットに示すように、[ **USB アプリケーション1パッケージのプロパティページ**] ウィンドウの左側のウィンドウで、[構成プロパティ] [ドライバー] [インストール] [ ** &gt; &gt; デプロイ**] の順に移動します。
  7. **[展開前にドライバーの以前のバージョンを削除する]** チェック ボックスをオンにします。
  8. **[リモート コンピューター名]** については、テストとデバッグ用に構成したコンピューターの名前を選んでください。 この演習では、dbg-target という名前のコンピューターを使用します。
  9. [**インストール/再インストールと検証**] を選択します。 **[適用]** をクリックします。

        ![winusb テンプレートの展開](images/winusb-template-deployment.png)

  10. 次のスクリーンショットに示すように、[プロパティ] ページで、[**構成プロパティ] [ &gt; デバッグ**] に移動し、[ **Windows 用デバッグツール–リモートデバッガー**] を選択します。

        ![winusb テンプレートリモートデバッガー](images/winusb-template-remote-debugger.png)

  11. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。 Visual Studio の [**出力**] ウィンドウにビルドの進行状況が表示されます。 (**出力**ウィンドウが表示されていない場合は、[**表示**] メニューの [**出力**] をクリックします)。この演習では、Windows 10 を実行する x64 システム用のプロジェクトをビルドしました。
  12. [**ビルド**] メニューの [**ソリューションの配置**] をクリックします。

ターゲットコンピューターで、ドライバーインストールスクリプトが実行されていることを確認します。 ドライバーファイルは、ターゲットコンピューターの% Systemdrive% \\ drivertest drivers フォルダーにコピーされ \\ ます。 .inf、.cat、test cert、.sys など、必要なファイルがすべて %systemdrive%\\drivertest\\drivers フォルダーに存在することを確認します。 デバイスは、エラーなしでデバイスマネージャーに表示される必要があります。

ホストコンピューターで、[**出力**] ウィンドウにこのメッセージが表示されます。

```syntax
Deploying driver files for project
"<path>\visual studio 14\Projects\USB Application1\USB Application1 Package\USB Application1 Package.vcxproj".  
Deployment may take a few minutes...
========== Build: 1 succeeded, 0 failed, 1 up-to-date, 0 skipped ==========
```

### <a name="to-debug-the-application"></a>アプリケーションをデバッグするには

1. ホストコンピューターで、ソリューションフォルダー内の**x64 &gt; Win 8.1 デバッグ**に移動します。
2. アプリケーションの実行可能ファイルを対象のコンピューターにコピーし UsbApplication1.exe ます。
3. ターゲットコンピューターで、アプリケーションを起動します。
4. ホストコンピューターで、[**デバッグ**] メニューの [**プロセスにアタッチ**] をクリックします。
5. ウィンドウで、トランスポートとして [ **Windows ユーザーモードデバッガー** (windows のデバッグツール)] を選択し、次の図に示すように、修飾子としてターゲットコンピューターの名前 (この場合は [dbg-target]) を選択します。

    ![winusb テンプレートのデバッグ設定](images/winusb-template6.png)

6. **利用可能なプロセス**の一覧からアプリケーションを選択し、[**アタッチ**] をクリックします。 **イミディエイトウィンドウ**を使用するか、[**デバッグ**] メニューのオプションを使用してデバッグできるようになりました。

上記の手順では、 **Windows 用デバッグツール–リモートデバッガー**を使用してアプリケーションをデバッグします。 **リモート Windows デバッガー** (Visual Studio に含まれるデバッガー) を使用する場合は、次の手順に従います。

1. ターゲットコンピューターで、ファイアウォールで許可されているアプリの一覧に msvsmon.exe を追加します。
2. C: drivertest msvsmonmsvsmon.exe にある Visual Studio リモートデバッグモニターを起動 \\ \\ \\ します。
3. C: remotetemp などの作業フォルダーを作成し \\ ます。
4. アプリケーションの実行可能ファイルをコピーして、ターゲットコンピューターの作業フォルダーに UsbApplication1.exe します。
5. ホストコンピューターの Visual Studio で、[ **USB アプリケーション 1 Package** ] プロジェクトを右クリックし、[**プロジェクトのアンロード**] を選択します。
6. [ **USB アプリケーション 1** ] プロジェクトを右クリックし、[プロジェクトのプロパティ] で [**構成プロパティ**] ノードを展開して、[**デバッグ**] をクリックします。
7. **リモート Windows デバッガー**に**起動するようにデバッガー**を変更します。
8. 「ローカルでビルドされた[プロジェクトのリモートデバッグ](https://docs.microsoft.com/visualstudio/debugger/remote-debugging?view=vs-2015)」に記載されている手順に従って、リモートコンピューターで実行可能ファイルを実行するようにプロジェクトの設定を変更します。 **作業ディレクトリ**と**リモートコマンド**のプロパティに、対象のコンピューター上のフォルダーが反映されていることを確認してください。
9. アプリケーションをデバッグするには、[**ビルド**] メニューの [**デバッグの開始**] をクリックするか、F5 キーを押し**ます。**

- **単一コンピューターのセットアップ:**

  1. アプリケーションとドライバーのインストールパッケージをビルドするには、[**ビルド**] メニューの [**ソリューションのビルド**] をクリックします。 Visual Studio の [**出力**] ウィンドウにビルドの進行状況が表示されます。 (**出力**ウィンドウが表示されていない場合は、[**表示**] メニューの [**出力**] をクリックします)。この演習では、Windows 10 を実行する x64 システム用のプロジェクトをビルドしました。
  2. ビルドされたドライバーパッケージを表示するには、Windows エクスプローラーで USB アプリケーション1フォルダーに移動し、[ **x64 \> Debug \> usb アプリケーション 1 package**] に移動します。 ドライバーパッケージには、いくつかのファイルが含まれています。 MyDriver .inf は、Windows がドライバーのインストール時に使用する情報ファイルです。 mydriver.cat は、インストーラーがドライバーパッケージのテスト署名を検証するために使用するカタログファイルです。 これらのファイルを次のスクリーンショットに示します。

        ![winusb アプリケーションテンプレート](images/winusb-template3.png)

        **メモ** パッケージにドライバーファイルが含まれていません。 これは、INF ファイルが Windows System32 フォルダーにあるインボックスドライバー Winusb.sys を参照しているためです \\ 。
  3. ドライバーを手動でインストールします。 デバイスマネージャーで、パッケージで INF を指定してドライバーを更新します。 前のセクションで示した、ソリューションフォルダーにあるドライバーパッケージをポイントします。
  4. [ **USB アプリケーション 1** ] プロジェクトを右クリックし、[プロジェクトのプロパティ] で [**構成プロパティ**] ノードを展開して、[**デバッグ**] をクリックします。
  5. **ローカル Windows デバッガー**に**起動するようにデバッガー**を変更します。
  6. [USB アプリケーション 1 Package] プロジェクトを右クリックし、[**プロジェクトのアンロード**] を選択します。
  7. アプリケーションをデバッグするには、[**ビルド**] メニューの [**デバッグの開始**] をクリックするか、 **F5**キーを押します。

## <a name="template-code-discussion"></a>テンプレートコードの説明

このテンプレートは、デスクトップアプリケーションの開始点となります。 USB アプリケーション1プロジェクトには、ソースファイルのデバイス .cpp とメイン .cpp があります。

メインの .cpp ファイルには、アプリケーションのエントリポイント tmain が含まれています。 \_ デバイスにハンドルを開いたり閉じたりするすべてのヘルパー関数が、デバイス .cpp に含まれています。

このテンプレートには、デバイス .h という名前のヘッダーファイルもあります。 このファイルには、デバイスインターフェイス GUID (後で説明します) と、 \_ アプリケーションによって取得された情報を格納するデバイスデータ構造の定義が含まれています。 たとえば、OpenDevice によって取得され、後続の操作で使用される WinUSB インターフェイスハンドルを格納します。

```cpp
typedef struct _DEVICE_DATA {

    BOOL                    HandlesOpen;
    WINUSB_INTERFACE_HANDLE WinusbHandle;
    HANDLE                  DeviceHandle;
    TCHAR                   DevicePath[MAX_PATH];

} DEVICE_DATA, *PDEVICE_DATA;
```

### <a name="getting-the-instance-path-for-the-device---see-retrievedevicepath-in-devicecpp"></a>デバイスのインスタンスパスを取得しています。 RetrieveDevicePath の「」を参照してください。

アプリケーションは、USB デバイスにアクセスするために、 **CreateFile**を呼び出すことによって、デバイスの有効なファイルハンドルを作成します。 その呼び出しに対して、アプリケーションはデバイスパスのインスタンスを取得する必要があります。 デバイスパスを取得するために、アプリは、 [setupapi.log](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)ルーチンを使用して、Winusb.sys のインストールに使用された INF ファイル内のデバイスインターフェイス GUID を指定します。 Device .h は、GUID devinterface USBApplication1 という名前の GUID 定数を宣言します。 \_ \_ これらのルーチンを使用すると、アプリケーションは、指定されたデバイスインターフェイスクラス内のすべてのデバイスを列挙し、デバイスのデバイスパスを取得します。

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

上記の関数では、アプリケーションは次のルーチンを呼び出してデバイスパスを取得します。

1. [**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)は、*デバイス情報セット*のハンドルを取得します。これは、指定したデバイスインターフェイスクラス GUID devinterface USBApplication1 に一致したすべてのインストール済みデバイスに関する情報を格納する配列 \_ \_ です。 *デバイスインターフェイス*と呼ばれる配列内の各要素は、システムにインストールされ、登録されているデバイスに対応します。 デバイスインターフェイスクラスは、INF ファイルで定義したデバイスインターフェイス GUID を渡すことによって識別されます。 関数は、デバイス情報セットへの HDEVINFO ハンドルを返します。
2. [**Setupdienumdeviceinterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) 。デバイス情報セット内のデバイスインターフェイスを列挙し、デバイスインターフェイスに関する情報を取得します。

    この呼び出しには、次の項目が必要です。

   - **CbSize**メンバーが構造体のサイズに設定されている、初期化された呼び出し元割り当て済み[**SP \_ デバイス \_ インターフェイス \_ データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)構造体。
   - 手順 1. の HDEVINFO ハンドル。
   - INF ファイルで定義したデバイスインターフェイス GUID。

    [**Setupdienumdeviceinterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)は、デバイスインターフェイスの指定したインデックスのデバイス情報セット配列を検索し、初期化された[**SP \_ デバイス \_ インターフェイスの \_ データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)構造に、インターフェイスに関する基本データを入力します。

    **メモ**  デバイス情報セット内のすべてのデバイスインターフェイスを列挙するには、関数が**FALSE**を返し、エラーのエラーコードが "その他の項目はありません" になるまで、ループで[**Setupdienumdeviceinterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)を呼び出します \_ \_ \_ 。 このエラーは、 \_ \_ \_ **GetLastError**を呼び出すことによって、他の項目のエラーコードを取得できません。 各反復処理で、メンバーインデックスをインクリメントします。

    または、デバイス情報セットを列挙する[**SetupDiEnumDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)を呼び出し、インデックスによって指定されたデバイスインターフェイス要素に関する情報を、呼び出し元が割り当てた[**SP \_ DEVINFO \_ データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)構造体に返すこともできます。 その後、 [**Setupdienumdeviceinterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)関数の*deviceinfodata*パラメーターでこの構造体への参照を渡すことができます。

3. [**Setupdigetdeviceinterfacedetail**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)を使用して、デバイスインターフェイスの詳細なデータを取得します。 情報は、 [**SP \_ デバイス \_ インターフェイスの \_ 詳細 \_ データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_detail_data_a)構造で返されます。 **SP \_ デバイス \_ インターフェイスの \_ 詳細 \_ データ**構造のサイズが異なるため、 **setupdigetdeviceinterfacedetail**は2回呼び出されます。 最初の呼び出しでは、 **SP \_ デバイス \_ インターフェイスの \_ 詳細 \_ データ**構造に割り当てるバッファーサイズを取得します。 2番目の呼び出しは、割り当てられたバッファーにインターフェイスに関する詳細情報を入力します。
   1. *Deviceinterfacedetail data*パラメーターが**NULL**に設定された[**Setupdigetdeviceinterfacedetail**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)を呼び出します。 関数は、 *requiredlength*パラメーターの正しいバッファーサイズを返します。 この呼び出しは、エラーが発生した \_ \_ バッファーエラーコードで失敗します。 このエラーコードは想定されています。
   2. *Requiredlength*パラメーターで取得される正しいバッファーサイズに基づいて、 [**SP \_ デバイス \_ インターフェイスの \_ 詳細 \_ データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_detail_data_a)構造にメモリを割り当てます。
   3. [**Setupdigetdeviceinterfacedetail**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)をもう一度呼び出し、 *Deviceinterfacedetail data*パラメーターで初期化された構造体への参照を渡します。 関数から制御が戻ると、インターフェイスに関する詳細情報が構造体に格納されます。 デバイスパスは、 [**SP \_ デバイスインターフェイスの \_ \_ 詳細 \_ データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_detail_data_a)構造の**DevicePath**メンバーに含まれています。

### <a name="creating-a-file-handle-for-the-device"></a>デバイスのファイルハンドルの作成

「デバイス .cpp の OpenDevice」を参照してください。

デバイスと対話するために、はデバイスの最初の (既定の) インターフェイスへの WinUSB インターフェイスハンドルを必要とします。 テンプレートコードは、ファイルハンドルと WinUSB インターフェイスハンドルを取得し、デバイスデータ構造に格納し \_ ます。

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

1. アプリは**CreateFile**を呼び出して、以前に取得したデバイスパスを指定することによって、デバイスのファイルハンドルを作成します。 \_ \_ Winusb がこの設定に依存しているため、ファイルフラグのオーバーラップフラグが使用されます。
2. デバイスのファイルハンドルを使用すると、アプリによって WinUSB インターフェイスハンドルが作成されます。 [Winusb 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)は、このハンドルを使用して、ファイルハンドルではなくターゲットデバイスを識別します。 WinUSB インターフェイスハンドルを取得するために、アプリはファイルハンドルを渡すことによって[**winusb \_ Initialize**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)を呼び出します。 その後の呼び出しで received ハンドルを使用して、デバイスから情報を取得し、デバイスに i/o 要求を送信します。

### <a name="release-the-device-handles---see-closedevice-in-devicecpp"></a>デバイスハンドルを解放する-「デバイス. .cpp の CloseDevice」を参照してください。

テンプレートコードは、ファイルハンドルを解放するコードと、デバイスの WinUSB インターフェイスハンドルを実装します。

- **CloseHandle**を使用して、このチュートリアルの「[デバイスのファイルハンドルを作成](#creating-a-file-handle-for-the-device)する」で説明されているように、 **CreateFile**によって作成されたハンドルを解放します。
- [**WinUsb\_Free**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free): デバイスの WinUSB インターフェイス ハンドルを解放します。これは、[**WinUsb\_Initialize**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize) によって返されます。

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

## <a name="next-steps"></a>次のステップ

次に、次のトピックを読んで、デバイス情報を取得し、データ転送をデバイスに送信します。

- [WinUSB 機能を使用して USB デバイスにアクセスする](using-winusb-api-to-communicate-with-a-usb-device.md)

    デバイス速度、インターフェイス記述子、関連するエンドポイント、パイプなど、USB 固有の情報をデバイスに照会する方法について説明します。

- [WinUSB デスクトップ アプリから USB 等時性転送を送信する](getting-set-up-to-use-windows-devices-usb.md)

    USB デバイスのアイソクロナスエンドポイントとの間でデータを転送します。

## <a name="related-topics"></a>関連トピック

[USB デバイス用の Windows デスクトップ アプリ](windows-desktop-app-for-a-usb-device.md)  
[ドライバーの展開とテスト用にコンピューターをプロビジョニングする](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)  

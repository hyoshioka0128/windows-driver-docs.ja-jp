---
Description: C と C++ WinUSB テンプレートを使用、USB デバイスと通信する Windows デスクトップ アプリを作成する最も簡単な方法です。
title: WinUSB テンプレートに基づいて Windows デスクトップ アプリを記述する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa5bbc2185d1e38b494f6e55315339480b7159af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324522"
---
# <a name="write-a-windows-desktop-app-based-on-the-winusb-template"></a>WinUSB テンプレートに基づいて Windows デスクトップ アプリを記述する


**重要な API**

-   [SetupAPI 関数](https://msdn.microsoft.com/library/windows/hardware/ff550855)
-   [WinUSB 関数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)

C と C++ WinUSB テンプレートを使用、USB デバイスと通信する Windows デスクトップ アプリを作成する最も簡単な方法です。 このテンプレートでは、Windows Driver Kit (WDK) (デバッグ ツールの Windows) で、Microsoft Visual Studio (Professional または Ultimate) との統合環境が必要です。 開始点としては、テンプレートを使用することができます。

## <a name="prerequisites"></a>前提条件


-   統合開発環境を設定するに最初に Microsoft Visual Studio Ultimate 2012 または Microsoft Visual Studio Professional 2012 をインストールし、WDK をインストールし。 Visual Studio と WDK の入手方法について詳しくは、[こちら](https://go.microsoft.com/fwlink/p/?linkid=239721)をご覧ください。
-   WDK をインストールするときに、デバッグ ツールの Windows が含まれます。 詳細については、次を参照してください。[ダウンロードとデバッグ ツールの Windows にインストール](https://go.microsoft.com/fwlink/p/?linkid=235427)します。

## <a name="creating-a-winusb-application"></a>WinUSB アプリケーションを作成します。


テンプレートからアプリケーションの作成。

1.  Microsoft Visual Studio を開きます。 **ファイル**] メニューの [選択**新規** &gt; **プロジェクト**します。 **新しいプロジェクト** ダイアログ ボックスが開いたら、次のスクリーン ショットに示すようにします。
2.  **新しいプロジェクト** ダイアログ ボックスで、左側のウィンドウで検索して選択**USB**します。
3.  中央のペインで選択**WinUSB アプリケーション。**
4.  **名前**フィールドにする場合は、プロジェクト名を変更します。 このトピックでは、既定の名前を使用します。
5.  **[場所]** フィールドに、新規プロジェクトを作るディレクトリを入力します。
6.  **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。 **[OK]** をクリックします。

    ![visual studio で winusb テンプレート](images/winusb-template.png)

    Visual Studio では、2 つのプロジェクトとソリューションを作成します。 ソリューション、2 つのプロジェクト内の各プロジェクトに属するファイルを確認できます、**ソリューション エクスプ ローラー**ウィンドウで、次のスクリーン ショットに示すようにします。 (**[ソリューション エクスプローラー]** ウィンドウが表示されない場合は、**[表示]** メニューの **[ソリューション エクスプローラー]** を選びます)。ソリューションには、USB Application1 および USB Application1 パッケージをという名前のドライバー パッケージ プロジェクトをという名前の C++ アプリケーション プロジェクトが含まれています。 アプリケーション ソース コードを確認する場合は、下に表示されるファイルのいずれかを開くことができます**ソースファイル**します。

    ![winusb テンプレート ソリューション エクスプ ローラー](images/winusb-template1.png)

    USB Application1 プロジェクトには、アプリケーションのソース ファイルが含まれます。

    USB Application1 パッケージ プロジェクトには、デバイス ドライバーとして Microsoft が提供 Winusb.sys ドライバーをインストールするために使用される INF ファイルが含まれています。

7.  USBApplication1.inf、INF ファイルでは、これらの行を見つけます。

    `%DeviceName% =USB_Install, USB\VID_vvvv&PID_pppp`

8.  VID を置き換える\_vvvv & PID\_pppp デバイスのハードウェア ID を使用します。 デバイス マネージャーから、ハードウェア ID を取得します。 デバイス マネージャーでは、デバイスのプロパティを表示します。 **詳細** タブで、表示、**ハードウェア Id**プロパティの値。
9.  **ソリューション エクスプ ローラー**ウィンドウで、右クリックして**ソリューション ' USB Application1' (2 プロジェクト)**、選択**Configuration Manager**します。 構成と、アプリケーション プロジェクトとパッケージのプロジェクトの両方のプラットフォームを選択します。 この演習で選択 Win8.1 デバッグおよび x64 では、次のスクリーン ショットに示すようにします。

    ![winusb アプリケーション テンプレート](images/winusb-template2.png)

## <a name="building-deploying-and-debugging-the-project"></a>ビルド、配置、およびプロジェクトのデバッグ


これまでに、この演習では、プロジェクトをビルドするのに Visual Studio を使用しました。 次に、デバイスが接続されているデバイスを構成する必要があります。 テンプレートでは、デバイスのドライバーとして Winusb ドライバーがインストールされていることが必要です。

テストとデバッグ環境を持つことができます。

-   2 つのコンピューターのセットアップ: ホスト コンピューターと対象コンピューター。 開発およびホスト コンピューターで Visual Studio でプロジェクトをビルドするとします。 デバッガーはホスト コンピューター上で実行され、Visual Studio のユーザー インターフェイスで利用できます。 テスト アプリケーションをデバッグすると、ターゲット コンピューターでドライバーを実行します。

-   1 台のコンピューターのセットアップ:1 台のコンピューターで、ターゲットとホストを実行します。 Visual Studio でプロジェクトをビルドを開発し、デバッガーとアプリケーションを実行します。

展開してインストール、読み込むには、するか、および次の手順に従って、アプリケーションとドライバーをデバッグすることができます。

-   **2 つのコンピューターのセットアップ**

    1.  次の手順で、対象のコンピュータをプロビジョニング[ドライバーの展開とテスト用にプロビジョニング](https://msdn.microsoft.com/library/windows/hardware/dn745909)します。
        **注:**  
        プロビジョニングすると、WDKRemoteUser という名前のターゲット コンピューターで、ユーザーが作成されます。 プロビジョニングが完了したら、WDKRemoteUser に切り替え、ユーザーが表示されます。 
    2.  ホスト コンピューター上で、Visual Studio でソリューションを開きます。
    3.  Main.cpp では、OpenDevice の呼び出しの前にこの行を追加します。

        `system ("pause")`

        行は、アプリケーションを起動したときに一時停止です。 これは、リモート デバッグで役に立ちます。

    4.  Pch.h には、この行を含めます。

        `#include <cstdlib>`

        これは、ステートメントの前の手順で system() 呼び出しが必要です。

    5.  **ソリューション エクスプ ローラー** USB Application1 パッケージを右クリックして、ウィンドウ、**プロパティ**します。
    6.  **USB Application1 パッケージのプロパティ ページ**に移動します ウィンドウの左側のウィンドウで、**構成プロパティ&gt;ドライバー インストール&gt;展開**ように、次のスクリーン ショット。
    7.  確認**展開を有効にする**、確認と**展開する前に以前のバージョンを削除**します。
    8.  **[リモート コンピューター名]** については、テストとデバッグ用に構成したコンピューターの名前を選んでください。 この演習では、dbg ターゲットをという名前のコンピューターを使用します。
    9.  **[Install and Verify (インストールと確認)]** を選びます。 **[OK]** をクリックします。

        ![winusb テンプレート](images/winusb-template4.png)

    10. プロパティ ページに移動します**構成プロパティ&gt;デバッグ**を選択し、**デバッグ ツールの Windows – リモート デバッガー**の次のスクリーン ショットに示すようにします。

        ![winusb テンプレートのデバッグ設定](images/winusb-template5.png)

    11. 選択**ソリューションのビルド**から、**ビルド**メニュー。 Visual Studio に表示されるビルドの進行状況、**出力**ウィンドウ。 (**[出力]** ウィンドウが表示されていない場合は、**[表示]** メニューの **[出力]** をクリックします)。この演習では、x-64 Windows 8.1 を実行しているシステムのプロジェクトをビルドしましたしました。

ターゲット コンピューターで実行されているドライバーのインストール スクリプトが表示されます。 %Systemdrive% に、ドライバー ファイルがコピーされます\\drivertest\\ターゲット コンピューター上のドライバー フォルダー。 .inf、.cat、test cert、.sys など、必要なファイルがすべて %systemdrive%\\drivertest\\drivers フォルダーに存在することを確認します。 デバイスは、エラーなしでデバイス マネージャーを表示する必要があります。

ホスト コンピューターでは、このメッセージが表示されます、**出力**ウィンドウ。

```syntax
Deploying driver files for project 
"<path>\visual studio 12\Projects\USB Application1\USB Application1 Package\USB Application1 Package.vcxproj".  
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
8.  記載されている手順に従って、リモート コンピューターで実行可能ファイルを実行するプロジェクト設定を変更[、プロジェクト ビルドのローカルのリモート デバッグ](https://msdn.microsoft.com/library/vstudio/8x6by8d2.aspx)します。 確認します**作業ディレクトリ**と**リモート コマンド**プロパティには、ターゲット コンピューターのフォルダーが反映されます。
9.  アプリケーションのデバッグ、**ビルド**メニューの [**デバッグの開始]**、またはキーを押します**f5 キー。**

-   **1 台のコンピューターのセットアップ:**

    1.  アプリケーションとドライバーのインストール パッケージをビルドするには、選択**ソリューションのビルド**から、**ビルド**メニュー。 Visual Studio に表示されるビルドの進行状況、**出力**ウィンドウで、次のスクリーン ショットに示すようにします。 (**[出力]** ウィンドウが表示されていない場合は、**[表示]** メニューの **[出力]** をクリックします)。この演習では、x-64 Windows 8.1 を実行しているシステムのプロジェクトをビルドしましたしました。
    2.  パッケージ化、Windows エクスプ ローラーで、USB Application1 フォルダーに移動しますおよびに移動し、構築されたドライバーを表示する**x64 &gt; Win8.1Debug &gt; USB Application1 パッケージ**します。 ドライバー パッケージには、いくつかのファイルが含まれています。USBApplication1.inf はドライバーをインストールするときに、Windows が使用する情報ファイルで、usbapplication1.cat はインストーラーを使用してドライバー パッケージのテスト署名を検証するカタログ ファイルです。 その他のファイルは、Windows Driver Frameworks (WDF) の共同インストーラーです。 これらのファイルは、次のスクリーン ショットに表示されます。

        ![winusb アプリケーション テンプレート](images/winusb-template3.png)

        **注**パッケージに含まれるドライバー ファイルがありません。 INF ファイルは、Windows で検出されたインボックス ドライバー Winusb.sys を参照しているためにである\\System32 フォルダー。
    3.  ドライバーを手動でインストールします。 デバイス マネージャーでは、パッケージに、INF を指定することで、ドライバーを更新します。 前のセクションで示すようにソリューション フォルダーにあるドライバ パッケージ をポイントします。
    4.  右クリックし、 **USB Application1**プロジェクトで、プロジェクトのプロパティで、展開、**構成プロパティ**ノードをクリックします**デバッグ**します。
    5.  変更**起動するデバッガー**に**ローカル Windows デバッガー**します。
    6.  7.  USB Application1 パッケージ プロジェクトを右クリックして**プロジェクトのアンロード**します。
    8.  アプリケーションのデバッグ、**ビルド**メニューの [**デバッグの開始]**、またはキーを押します**f5 キーを押して**します。

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

USB デバイスへのアクセス、アプリケーションでは、呼び出すことによって、デバイスの有効なファイル ハンドルを作成**CreateFile**します。 その呼び出しでは、アプリケーションがデバイス パスのインスタンスを取得する必要があります。 アプリでは、デバイス パスを取得する[SetupAPI](https://msdn.microsoft.com/library/windows/hardware/ff550855)ルーチンを Winusb.sys のインストールに使用された INF ファイルで、デバイス インターフェイスの GUID を指定します。 GUID を名前付き GUID 定数を宣言する Device.h\_DEVINTERFACE\_USBApplication1 します。 これらのルーチンを使用するは、アプリケーションは、指定したデバイスのインターフェイス クラスのすべてのデバイスを列挙し、デバイスのデバイス パスを取得します。

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

1.  [**SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551072)を識別するハンドルを取得する、*デバイス情報設定されている*、指定したデバイスのインターフェイス クラス GUIDに一致するすべてのインストールされているデバイスに関する情報を格納する配列\_DEVINTERFACE\_USBApplication1 します。 配列内の各要素と呼ばれる、*デバイス インターフェイス*がインストールされ、システムに登録されているデバイスに対応しています。 デバイスのインターフェイス クラスは、デバイス インターフェイス INF ファイルで定義した GUID を渡すことによって識別されます。 関数は、デバイス情報のセットに HDEVINFO ハンドルを返します。
2.  [**SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)デバイスを列挙するインターフェイスでデバイス情報設定し、デバイス インターフェイスに関する情報を取得します。

    この呼び出しでは、次のものが必要です。

    -   初期化された呼び出し元が割り当てた[ **SP\_デバイス\_インターフェイス\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff552342)構造を持つその**cbSize**メンバーに設定構造体のサイズ。
    -   手順 1 から HDEVINFO ハンドル。
    -   デバイスのインターフェイスの INF ファイルで定義した GUID です。

    [**SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)デバイス インターフェイスの指定したインデックスのデバイス情報設定の配列を検索し、初期化された入力[ **SP\_デバイス\_インターフェイス\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff552342)インターフェイスに関する基本的なデータを含む構造体。

    **注**デバイス情報のセット内のすべてのデバイス インターフェイスを列挙するために呼び出す[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)関数が戻るまでループで**FALSE**障害のエラー コードはエラーと\_いいえ\_詳細\_項目。 エラー\_いいえ\_詳細\_項目のエラー コードを呼び出すことによって取得できる**GetLastError**します。 反復処理ごとに、メンバーのインデックスをインクリメントします。

    または、呼び出せる[ **SetupDiEnumDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551010)するデバイス情報のセットを列挙し、呼び出し元が割り当てた内でのインデックスで指定された、デバイスのインターフェイス要素に関する情報を返します[ **SP\_DEVINFO\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff552344)構造体。 この構造体への参照を渡すことができますし、 *DeviceInfoData*のパラメーター、 [ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)関数。

3.  [**SetupDiGetDeviceInterfaceDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551120)デバイス インターフェイスの詳細なデータを取得します。 情報が返されます、 [ **SP\_デバイス\_インターフェイス\_詳細\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff552343)構造体。 のサイズ、 **SP\_デバイス\_インターフェイス\_詳細\_データ**構造の変化に合わせて、 **SetupDiGetDeviceInterfaceDetail**が呼び出されます2 回クリックします。 最初の呼び出しが用に割り当てるバッファーのサイズを取得、 **SP\_デバイス\_インターフェイス\_詳細\_データ**構造体。 2 番目の呼び出しでは、インターフェイスに関する詳しい情報を割り当てられたバッファーを設定します。
    1.  呼び出し[ **SetupDiGetDeviceInterfaceDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551120)で*DeviceInterfaceDetailData*パラメーターに設定**NULL**します。 関数が適切なバッファー サイズを返します、 *requiredlength*パラメーター。 この呼び出しがエラーで失敗\_不十分\_バッファーのエラー コード。 このエラー コードが必要です。
    2.  メモリを割り当て、 [ **SP\_デバイス\_インターフェイス\_詳細\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff552343)構造が取得される適切なバッファー サイズに基づいて、*requiredlength*パラメーター。
    3.  呼び出し[ **SetupDiGetDeviceInterfaceDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551120)もう一度で初期化された構造体への参照を渡すと、 *DeviceInterfaceDetailData*パラメーター。 関数から制御が戻るときに、構造体はインターフェイスに関する詳しい情報を入力されます。 デバイスのパスが、 [ **SP\_デバイス\_インターフェイス\_詳細\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff552343)構造体の**DevicePath**メンバー。

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
2.  ファイル ハンドルを使用すると、デバイス、アプリは WinUSB インターフェイスのハンドルを作成します。 [WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)ファイル ハンドルが、代わりに、ターゲット デバイスを識別するために、このハンドルを使用します。 WinUSB インターフェイス ハンドルをアプリの呼び出しを取得する[ **WinUsb\_初期化**](https://msdn.microsoft.com/library/windows/hardware/ff540277)ファイル ハンドルを渡すことによって。 I/O 要求をデバイスに送信して、デバイスから情報を取得、後続の呼び出しで受信したハンドルを使用します。

### <a name="release-the-device-handles---see-closedevice-in-devicecpp"></a>デバイス ハンドルのリリース - device.cpp CloseDevice を参照してください。

テンプレート コードでは、ファイル ハンドルとデバイスの WinUSB インターフェイスのハンドルを解放するコードを実装します。

-   **CloseHandle**によって作成されたハンドルを解放する**CreateFile**」の説明に従って、[ファイル ハンドルを作成、デバイスの](#filehandle)このチュートリアルの「します。
-   [**WinUsb\_Free** ](https://msdn.microsoft.com/library/windows/hardware/ff540233)によって返されると、デバイスの WinUSB インターフェイスのハンドルを解放する[ **WinUsb\_初期化**](https://msdn.microsoft.com/library/windows/hardware/ff540277)します。

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
[ドライバーの展開およびテスト用のコンピューターをプロビジョニングします。](https://msdn.microsoft.com/library/windows/hardware/dn745909)  




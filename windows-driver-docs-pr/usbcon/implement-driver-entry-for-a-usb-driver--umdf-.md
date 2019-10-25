---
Description: Microsoft Visual Studio に用意されている USB ユーザーモードドライバーテンプレートを使用して、UMDF クライアントドライバーを作成します。
title: 最初の USB クライアントドライバー (UMDF) を作成する方法
ms.date: 06/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: bfbe42db344877684761a07c1d1c92e2fcb96969
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838827"
---
# <a name="how-to-write-your-first-usb-client-driver-umdf"></a>最初の USB クライアントドライバー (UMDF) を作成する方法


このトピックでは、Microsoft Visual Studio 2019 に用意されている**USB ユーザーモードドライバー**テンプレートを使用して、ユーザーモードドライバーフレームワーク (UMDF) ベースのクライアントドライバーを記述します。 クライアントドライバーをビルドしてインストールした後、**デバイスマネージャー**でクライアントドライバーを表示し、デバッガーでドライバーの出力を表示します。

UMDF (このトピックではフレームワークと呼ばれます) は、コンポーネントオブジェクトモデル (COM) に基づいています。 既定では、すべてのフレームワークオブジェクトが[**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)とそのメソッド、 [**QueryInterface**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))、 [**AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)、および[**Release**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)を実装する必要があります。 **AddRef**メソッドと**Release**メソッドは、オブジェクトの有効期間を管理するため、クライアントドライバーは参照カウントを維持する必要がありません。 **QueryInterface**メソッドを使用すると、クライアントドライバーは、Windows driver FRAMEWORK (WDF) オブジェクトモデル内の他のフレームワークオブジェクトへのインターフェイスポインターを取得できます。 フレームワークオブジェクトは、複雑なドライバータスクを実行し、Windows と対話します。 特定のフレームワークオブジェクトは、クライアントドライバーがフレームワークと対話できるようにするインターフェイスを公開します。

UMDF ベースのクライアントドライバーは、インプロセス COM サーバー (DLL) として実装されますC++ 。これは、USB デバイス用のクライアントドライバーを記述するときに推奨される言語です。 通常、クライアントドライバーは、フレームワークによって公開されるいくつかのインターフェイスを実装します。 このトピックでは、コールバッククラスとしてフレームワークインターフェイスを実装するクライアントドライバー定義のクラスについて説明します。 これらのクラスがインスタンス化されると、結果として得られるコールバックオブジェクトは、特定のフレームワークオブジェクトと提携されます。 このパートナーシップにより、クライアントドライバーは、フレームワークによって報告されたデバイスまたはシステム関連のイベントに応答できるようになります。 Windows が特定のイベントについてフレームワークに通知するたびに、フレームワークはクライアントドライバーのコールバックを呼び出します (使用可能な場合)。 それ以外の場合、フレームワークはイベントの既定の処理を続行します。 テンプレートコードは、ドライバー、デバイス、およびキューのコールバッククラスを定義します。

テンプレートによって生成されるソースコードの説明については、「 [USB クライアントドライバーの UMDF テンプレートコード](understanding-the-umdf-template-code-for-usb.md)について」を参照してください。

### <a name="prerequisites"></a>前提条件

ユーザーモードドライバーを開発、デバッグ、およびインストールするには、次の2つのコンピューターが必要です。

-   Windows 7 以降のバージョンの Windows オペレーティングシステムを実行しているホストコンピューター。 ホストコンピューターは開発環境で、ドライバーを記述してデバッグします。
-   ドライバーをテストするオペレーティングシステムのバージョンを実行しているターゲットコンピューター (Windows 10、バージョン1903など)。 対象のコンピューターには、デバッグ対象のユーザーモードドライバーと、デバッガーの1つがあります。

ホストとターゲットコンピューターが同じバージョンの Windows を実行している場合、windows 7 以降のバージョンの Windows を実行しているコンピューターを1台だけ使用することができます。 このトピックでは、ユーザーモードドライバーの開発、デバッグ、およびインストールに2台のコンピューターを使用していることを前提としています。

開始する前に、次の要件を満たしていることを確認してください。

**ソフトウェア要件**

-   ホストコンピューターに Visual Studio 2019 がある。
-   ホストコンピューターには、Windows 10 バージョン1903用の最新の Windows Driver Kit (WDK) が搭載されています。

    キットには、USB クライアントドライバーの開発、ビルド、およびデバッグに必要なヘッダー、ライブラリ、ツール、ドキュメント、およびデバッグツールが含まれています。 Wdk の最新バージョンは、「 [wdk の入手方法](https://go.microsoft.com/fwlink/p/?linkid=617585)」から入手できます。

-   ホストコンピューターには、Windows 用デバッグツールの最新バージョンが搭載されています。 WDK から最新バージョンを入手することも、 [Windows 用デバッグツールをダウンロードしてインストール](https://go.microsoft.com/fwlink/p/?linkid=617701)することもできます。
-   2台のコンピューターを使用している場合は、ユーザーモードのデバッグ用にホストとターゲットコンピューターを構成する必要があります。 詳細については、「 [Visual Studio でのユーザーモードデバッグの設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-user-mode-debugging-in-visual-studio)」を参照してください。

**ハードウェア要件**

クライアントドライバーを書き込む USB デバイスを取得します。 ほとんどの場合、USB デバイスとそのハードウェア仕様が用意されています。 この仕様では、デバイスの機能とサポートされているベンダーのコマンドについて説明します。 仕様を使用して、USB ドライバーの機能と関連する設計上の決定を決定します。

USB ドライバーの開発を初めて行う場合は、OSR USB FX2 learning kit を使用して、WDK に含まれている USB サンプルを調査してください。 この学習キットは、 [OSR オンライン](https://go.microsoft.com/fwlink/p/?linkid=617553)で入手できます。 このファイルには、USB FX2 デバイスと、クライアントドライバーを実装するために必要なすべてのハードウェア仕様が含まれています。

**推奨資料**

-   [すべてのドライバー開発者向けの概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)
-   [デバイスノードとデバイススタック](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)
-   [Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index)
-   [ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/debugger/user-mode-driver-framework-debugging)
-   *Windows Driver Foundation でのドライバーの開発*。これは、少額 Orwick と Guy Smith によって記述されています。 詳細については、「 [WDF を使用したドライバーの開発](https://go.microsoft.com/fwlink/p/?linkid=617702)」を参照してください。

<a name="instructions"></a>このサンプルについての指示
------------

### <a href="" id="generate-the-umdf-driver-code-by-using-the-visual-studio-2019-usb-driver-template"></a>手順 1: Visual Studio 2019 の USB ドライバーテンプレートを使用して UMDF ドライバーコードを生成する

<a href="" id="generate"></a>UMDF ドライバーコードを生成する手順については、「[テンプレートに基づく umdf ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-umdf-driver-based-on-a-template)」を参照してください。

**USB 固有のコードの場合は、Visual Studio 2019 で次のオプションを選択します。**

1.  **新しいプロジェクト** ダイアログボックスの上部にある 検索 ボックスに、「USB」と入力し**ます。**
2.  中央のウィンドウで、 **[ユーザーモードドライバー、USB (UMDF V2)]** を選択します。
3.  **[次へ]** をクリックします。
4.  プロジェクト名を入力し、保存場所を選択して、 **[作成]** をクリックします。

次のスクリーンショットは、 **USB ユーザーモードドライバー**テンプレートの **[新しいプロジェクト]** ダイアログボックスを示しています。

![visual studio の新しいプロジェクトオプション](images/umdf-template-visual-studio-2019.png)

![visual studio の [新しいプロジェクト] オプション2番目の画面](images/umdf-template-visual-studio-2019-2.png)

このトピックでは、プロジェクトの名前が "MyUSBDriver\_UMDF\_" であることを前提としています。 次のファイルが含まれています。

| ファイル                      | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Driver. h;Driver .c         | [**Idriverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)インターフェイスを実装するコールバッククラスを宣言して定義します。 クラスは、フレームワークの driver オブジェクトによって呼び出されるメソッドを定義します。 このクラスの主な目的は、クライアントドライバーのデバイスオブジェクトを作成することです。                                                                                                                                                                     |
| デバイス .h;Device. c         | [**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)インターフェイスを実装するコールバッククラスを宣言して定義します。 クラスは、フレームワークデバイスオブジェクトによって呼び出されるメソッドを定義します。 このクラスの主な目的は、プラグアンドプレイ (PnP) 状態の変更の結果として発生するイベントを処理することです。 また、クラスは、システムに読み込まれている限り、クライアントドライバーが必要とするリソースを割り当て、初期化します。 |
| IoQueue. h;IoQueue .c       | [**IQueueCallbackDeviceIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)インターフェイスを実装するコールバッククラスを宣言して定義します。 クラスは、フレームワークキューオブジェクトによって呼び出されるメソッドを定義します。 このクラスの目的は、フレームワークでキューに登録されている i/o 要求を取得することです。                                                                                                                               |
| 内部 .h                 | クライアントドライバーおよび USB デバイスと通信するユーザーアプリケーションによって共有される共通の宣言を提供します。 トレース関数とマクロも宣言します。                                                                                                                                                                                                                                                                          |
| Dllsup .cpp                 | ドライバーモジュールのエントリポイントの実装を格納します。                                                                                                                                                                                                                                                                                                                                                                              |
| *&lt;プロジェクト名&gt;* .inf | 対象のコンピュータにクライアントドライバをインストールするために必要な INF ファイル。                                                                                                                                                                                                                                                                                                                                                               |
| .Def をエクスポートします。                | ドライバーモジュールのエントリポイント関数名をエクスポートする DEF ファイル。                                                                                                                                                                                                                                                                                                                                                                    |

 

### <a href="" id="modify-the-inf-file-to-add-information-about-your-device"></a>手順 2: INF ファイルを変更してデバイスに関する情報を追加する

<a href="" id="modify"></a>ドライバーをビルドする前に、デバイスに関する情報 (具体的にはハードウェア ID 文字列) を使用して、テンプレートの INF ファイルを変更する必要があります。

**ハードウェア ID 文字列を指定するには**

1.  USB デバイスをホストコンピューターに接続し、Windows によってデバイスが列挙されるようにします。
2.  **デバイスマネージャー**を開いて、デバイスのプロパティを開きます。
3.  **[詳細]** タブで、プロパティ の下にある **[ハードワード id]** を選択し**ます。**

    デバイスのハードウェア ID がリストボックスに表示されます。 右クリックして、[ハードウェア ID] 文字列をコピーします。

4.  **ソリューションエクスプローラー**で、 **[ドライバーファイル]** を展開し、INF を開きます。
5.  次のハードウェア ID 文字列を置き換えます。

    `[Standard.NT$ARCH$]`

    `%DeviceName%=MyDevice_Install, USB\VID_vvvv&PID_pppp`

ドライバーの情報 (INF) ファイルに**AddReg**エントリがあることに注意してください。

`[CoInstallers_AddReg] ;`

`HKR,,CoInstallers32,0x00010008,"WudfCoinstaller.dll"`

`HKR,,CoInstallers32,0x00010008,"WudfUpdate_01011.dll"`

`HKR,,CoInstallers32,0x00010008,"WdfCoInstaller01011.dll,WdfCoInstaller"`

`HKR,,CoInstallers32,0x00010008,"WinUsbCoinstaller2.dll"`

- WudfCoinstaller インストーラー (構成の共同インストーラー)
- WUDFUpdate\_ *&lt;バージョン&gt;* .dll (再頒布可能な共同インストーラー)
- Wdfcoinstaller インストーラー<em>&lt;version&gt;</em>.DLL (kmdf の共同インストーラー)
- Winusbcoinstaller2 ((Winusb .sys 用の共同インストーラー)
- MyUSBDriver\_UMDF\_.dll (クライアントドライバーモジュール)

INF AddReg ディレクティブが、UMDF 再配布可能な共同インストーラー (WUDFUpdate\_ *&lt;バージョン&gt;* .dll) を参照している場合は、構成の共同インストーラー (wudfupdate .dll) への参照を作成することはできません。 INF で両方の共同インストーラーを参照すると、インストールエラーが発生します。

すべての UMDF ベースの USB クライアントドライバーには、2つの Microsoft 提供ドライバー (リフレクターと WinUSB) が必要です。

-   リフレクター: ドライバーが正常に読み込まれると、リフレクターはカーネルモードスタックの最上位のドライバーとして読み込まれます。 リフレクターは、カーネルモードスタックの最上位のドライバーである必要があります。 この要件を満たすには、テンプレートの INF ファイルで、リフレクターをサービスとして指定し、WinUSB を INF の下位フィルタードライバーとして指定します。

    `[MyDevice_Install.NT.Services]`

    `AddService=WUDFRd,0x000001fa,WUDFRD_ServiceInstall  ; flag 0x2 sets this as the service for the device`

    `AddService=WinUsb,0x000001f8,WinUsb_ServiceInstall  ; this service is installed because its a filter.`

-   WinUSB —インストールパッケージには、Winusb. sys の coinstallers が含まれている必要があります。これは、クライアントドライバーの場合、WinUSB はカーネルモードの USB ドライバースタックへのゲートウェイであるためです。 読み込まれるもう1つのコンポーネントは、クライアントドライバーのホストプロセス (Wudfhost .exe) にある WinUsb .dll というユーザーモードの DLL です。 Winusb .dll は、クライアントドライバーと WinUSB 間の通信プロセスを簡略化する[Winusb 機能](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を公開します。

### <a href="" id="build-the-usb-client-driver-code"></a>手順 3: USB クライアントドライバーコードを作成する

<a href="" id="build"></a>**ドライバーのビルド**


1.  Visual Studio 2019 でドライバープロジェクトまたはソリューションを開きます。
2.  **ソリューションエクスプローラー**でソリューションを右クリックし、 **[Configuration Manager]** を選択します。
3.  **Configuration Manager**から、**アクティブなソリューション構成**(**デバッグ**や**リリース**など) と、ビルドの種類に対応する**アクティブなソリューションプラットフォーム**( **Win32**など) を選択します。興味があります。
4.  デバイスインターフェイスの GUID がプロジェクト全体で正確であることを確認します。 
    - デバイスインターフェイス GUID は、resource.h で定義され、デバイス .c の `MyUSBDriverUMDFCreateDevice` から参照されます。 "MyUSBDriver\_UMDF\_" という名前のプロジェクトを作成すると、Visual Studio 2019 では、`GUID_DEVINTERFACE_MyUSBDriver_UMDF_` という名前のデバイスインターフェイス GUID が定義されますが、正しくないパラメーター "GUID_DEVINTERFACE_MyUSBDriverUMDF" を使用して `WdfDeviceCreateDeviceInterface` が呼び出されます。 正しくないパラメーターをトレースに定義されている名前に置き換えて、ドライバーが正常にビルドされるようにします。 
4.  **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

詳細については、「[ドライバーのビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)」を参照してください。

### <a href="" id="configure-a-computer-for-testing-and-debugging"></a>手順 4: テストおよびデバッグ用にコンピューターを構成する

ドライバーをテストしてデバッグするには、ホストコンピューター上でデバッガーを実行し、ターゲットコンピューターでドライバーを実行します。 ここまでで、ホストコンピューターで Visual Studio を使用してドライバーをビルドしました。 次に、対象のコンピューターを構成する必要があります。 ターゲットコンピューターを構成するには、「[ドライバーの展開およびテスト用のコンピューターのプロビジョニング](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の手順に従います。

### <a href="" id="enable-tracing-for-kernel-debugging"></a>手順 5: カーネルデバッグのトレースを有効にする

テンプレートコードには、関数呼び出しの追跡に役立つトレースメッセージ (TraceEvents) がいくつか含まれています。 ソースコード内のすべての関数には、ルーチンのエントリと終了をマークするトレースメッセージが含まれています。 エラーの場合、トレースメッセージにはエラーコードと意味のある文字列が含まれます。 ドライバープロジェクトでは、WPP トレースが有効になっているため、ビルド処理中に作成される PDB シンボルファイルには、トレースメッセージの書式設定命令が含まれます。 WPP トレース用にホストとターゲットコンピューターを構成した場合、ドライバーはトレースメッセージをファイルまたはデバッガーに送信できます。

**WPP トレース用にホストコンピューターを構成するには**

1. PDB シンボルファイルからトレースメッセージの書式設定命令を抽出して、トレースメッセージ形式 (TMF) ファイルを作成します。

   Tracepdb を使用して、TMF ファイルを作成できます。 このツールは、 <em>&lt;インストールフォルダー&gt;</em>Windows キット\\10\\bin\\ *&lt;architecture&gt;* フォルダーにあります。 次のコマンドは、ドライバープロジェクト用の TMF ファイルを作成します。

   **tracepdb-f \[PDBFiles\]-p \[TMFDirectory\]**

   **-F**オプションは、PDB シンボルファイルの場所と名前を指定します。 **-P**オプションは、tracepdb によって作成される tmf ファイルの場所を指定します。 詳細については、「 [**Tracepdb コマンド**](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracepdb-commands)」を参照してください。

   指定した場所に、3つのファイルが表示されます (プロジェクトの c ファイルごとに1つ)。 GUID ファイル名が与えられます。

2. デバッガーで、次のコマンドを入力します。
   1.  **. load Wmitrace**

       Wmitrace 拡張子を読み込みます。

   2.  **. チェーン**

       デバッガー拡張機能が読み込まれていることを確認します。

   3.  * *! wmitrace searchpath + * * *&lt;TMF ファイルの場所&gt;*

       TMF ファイルの場所をデバッガー拡張機能の検索パスに追加します。

       出力は次のようになります。

       `Trace Format search path is: 'C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE;c:\drivers\tmf'`

**WPP トレース用にターゲットコンピューターを構成するには**

1. ターゲットコンピューターに Tracelog ツールがインストールされていることを確認します。 このツールは、 <em>&lt;install\_フォルダー&gt;</em>Windows キット\\10\\ツール\\&lt;WDK *&gt;* フォルダーにあります。 詳細については、「 [**Tracelog コマンドの構文**](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog-command-syntax)」を参照してください。
2. **コマンドウィンドウ**を開き、管理者として実行します。
3. 次のコマンドを入力します。

   **トレースログ-開始 mytrace-guid \#c918ee71-68c7-4140-8f7d-c907abbcb05d-フラグ 0xffff-level 7-rt-kd**

   このコマンドは、MyTrace という名前のトレースセッションを開始します。

   **Guid**引数は、クライアントドライバーであるトレースプロバイダーの guid を指定します。 Visual Studio 2019 プロジェクトの resource.h から GUID を取得できます。 別のオプションとして、次のコマンドを入力し、guid ファイルに GUID を指定することもできます。 このファイルには、次のように、GUID がハイフン形式で含まれています。

   **トレースログ-開始 mytrace-guid c:\\drivers\\Provider. guid-flag 0xffff-level 7-rt-kd**

   次のコマンドを入力すると、トレースセッションを停止できます。

   **トレースログ-mytrace の停止**

### <a href="" id="deploy-the-driver-on-the-target-computer"></a>手順 6: ターゲットコンピューターにドライバーを展開する

1. **[ソリューションエクスプローラー]** ウィンドウで、[ <em>&lt;プロジェクト名&gt;</em>**パッケージ**] を右クリックし、 **[プロパティ]** を選択します。
2. 左側のウィンドウで、[**構成プロパティ] &gt; [ドライバー] [インストール &gt; の展開**] の順に移動します。
3. [展開の有効化] チェックボックスをオンにし、[ドライバーストアへのインポート] をオンにします。
4. **[リモートコンピューター名]** に、対象のコンピューターの名前を指定します。
5. **[インストールと確認]** を選択します。
6. **[OK]** をクリックします。
7. **[デバッグ]** メニューの **[デバッグの開始]** をクリックするか、キーボードの**F5**キーを押します。

**注**  **ハードウェア Id ドライバーの更新プログラム**では、デバイスのハードウェア id*を指定しないでください*。 ハードウェア ID は、ドライバーの情報 (INF) ファイルでのみ指定する必要があります。

 

### <a href="" id="view-the-driver-in-device-manager"></a>手順 7: デバイスマネージャーでドライバーを表示する

<a href="" id="devicemanager"></a>
1.  次のコマンドを入力して、**デバイスマネージャー**を開きます。

    **devmgmt.msc**

2.  **デバイスマネージャー**に次のノードが表示されていることを確認します。

    **USB デバイス**

    **MyUSBDriver\_UMDF\_デバイス**

### <a href="" id="view-the-output-in-the-debugger"></a>手順 8: デバッガーで出力を表示する

ホストコンピューターのデバッガーの [**イミディエイト] ウィンドウ**にトレースメッセージが表示されていることを確認します。

出力は次のようになります。

``` syntax
[0]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::OnPrepareHardware Entry
[0]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::OnPrepareHardware Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::CreateInstanceAndInitialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Initialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Initialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::CreateInstanceAndInitialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Configure Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::CreateInstanceAndInitialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::Initialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::Initialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::CreateInstanceAndInitialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Configure Exit
```

<a name="remarks"></a>解説
-------

フレームワークとクライアントドライバーがどのように連携して Windows とやり取りし、USB デバイスに送信された要求を処理するかを見てみましょう。 次の図は、UMDF ベースの USB クライアントドライバー用にシステムに読み込まれたモジュールを示しています。

![ユーザーモードクライアントドライバーのアーキテクチャ](images/umdfstack.png)

各モジュールの目的は次のとおりです。

-   アプリケーション-i/o 要求を発行して USB デバイスと通信するユーザーモードプロセス。
-   I/o マネージャー-受信したアプリケーション要求を表す i/o 要求パケット (Irp) を作成し、ターゲットデバイスのカーネルモードのデバイススタックの一番上に転送する Windows コンポーネントです。
-   リフレクター—カーネルモードのデバイススタック (WUDFRd .sys) の最上位にインストールされている、Microsoft が提供するカーネルモードドライバー。 リフレクターは、i/o マネージャーから受信した Irp をクライアントドライバーホストプロセスにリダイレクトします。 要求を受け取ったときに、フレームワークとクライアントドライバーが要求を処理します。
-   ホストプロセス—ユーザーモードドライバーを実行するプロセス (Wudfhost .exe)。 また、フレームワークと i/o ディスパッチャーもホストします。
-   クライアントドライバー-USB デバイス用のユーザーモード関数ドライバー。
-   UMDF: クライアントドライバーに代わって Windows とのほとんどのやり取りを処理するフレームワークモジュール。 これは、クライアントドライバーが一般的なドライバータスクを実行するために使用できるユーザーモードデバイスドライバーインターフェイス (DDIs) を公開します。
-   Dispatcher —ホストプロセスで実行されるメカニズム。ユーザーモードドライバーによって処理され、ユーザーモードスタックの一番下に到達した後に、要求をカーネルモードに転送する方法を決定します。 この図では、ディスパッチャーはユーザーモードの DLL である Winusb .dll に要求を転送します。
-   Winusb .dll-クライアントドライバーと WinUSB (Winusb .sys) の間の通信プロセスを簡略化する[Winusb 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を公開する、Microsoft が提供する、カーネルモードで読み込まれたユーザーモードの dll です。
-   Winusb .sys-USB デバイスのすべての UMDF クライアントドライバーで必要とされる、Microsoft 提供のドライバーです。 ドライバーはリフレクターの下にインストールする必要があり、カーネルモードの USB ドライバースタックへのゲートウェイとして機能します。 詳細については、「 [Winusb](winusb.md)」を参照してください。
-   USB ドライバースタック-Microsoft が提供する、USB デバイスとのプロトコルレベルの通信を処理するドライバーのセット。 詳細については、「 [Windows の USB ホスト側ドライバー](usb-3-0-driver-stack-architecture.md)」を参照してください。

アプリケーションが USB ドライバースタックの要求を行うたびに、Windows i/o マネージャーは、その要求をリフレクタに送信します。これにより、ユーザーモードでクライアントドライバーに要求が送信されます。 クライアントドライバーは、特定の UMDF メソッドを呼び出すことによって要求を処理します。このメソッドは、内部的に[Winusb 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を呼び出して winusb に要求を送信します。 WinUSB は、要求を受信すると、要求を処理するか、USB ドライバースタックに転送します。

## <a name="related-topics"></a>関連トピック
[USB クライアントドライバーの UMDF テンプレートコードについて](understanding-the-umdf-template-code-for-usb.md)  
[USB デバイスの UMDF ドライバーで USB セレクティブサスペンドとシステムウェイクを有効にする方法](https://go.microsoft.com/fwlink/p/?linkid=617587)  
[USB クライアントドライバー開発の概要](getting-started-with-usb-client-driver-development.md)  




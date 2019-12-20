---
Description: このトピックでは、Microsoft Visual Studio Professional 2019 に用意されている USB カーネルモードドライバーテンプレートを使用して、単純なカーネルモードドライバーフレームワーク (KMDF) ベースのクライアントドライバーを記述します。
title: 初めての USB クライアント ドライバーの記述方法 (KMDF)
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9363dc1d79f191c9ade7da2400b24272fa481ba6
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210620"
---
# <a name="how-to-write-your-first-usb-client-driver-kmdf"></a>初めての USB クライアント ドライバーの記述方法 (KMDF)


このトピックでは、Microsoft Visual Studio Professional 2019 に用意されている**USB カーネルモードドライバー**テンプレートを使用して、単純なカーネルモードドライバーフレームワーク (kmdf) ベースのクライアントドライバーを記述します。 クライアントドライバーをビルドしてインストールした後、**デバイスマネージャー**でクライアントドライバーを表示し、デバッガーでドライバーの出力を表示します。

テンプレートによって生成されるソースコードの説明については、「 [USB クライアントドライバーの KMDF テンプレートコード](understanding-the-kmdf-template-code-for-usb.md)について」を参照してください。

### <a name="prerequisites"></a>前提条件

カーネルモードドライバーを開発、デバッグ、およびインストールするには、次の2台のコンピューターが必要です。

-   Windows 7 以降のバージョンの Windows オペレーティングシステムを実行しているホストコンピューター。 ホストコンピューターは開発環境で、ドライバーを記述してデバッグします。
-   Windows Vista 以降のバージョンの Windows を実行しているターゲットコンピュータ。 ターゲットコンピューターには、デバッグするカーネルモードドライバーがあります。

開始する前に、次の要件を満たしていることを確認してください。

**ソフトウェア要件**

-   ホストコンピューターは開発環境をホストしており、Visual Studio Professional 2019 があります。
-   ホストコンピューターには、Windows 8 用の最新の Windows Driver Kit (WDK) が搭載されています。 キットには、KMDF ドライバーの開発、ビルド、およびデバッグに必要なヘッダー、ライブラリ、ツール、ドキュメント、およびデバッグツールが含まれています。 最新バージョンの WDK を入手するには、「 [Windows Driver Kit (wdk) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)」を参照してください。
-   ホストコンピューターには、Windows 用デバッグツールの最新バージョンが搭載されています。 WDK から最新バージョンを入手することも、 [Windows 用デバッグツールをダウンロードしてインストール](https://msdn.microsoft.com/windows/hardware/gg463009.aspx)することもできます。
-   対象のコンピューターで Windows Vista 以降のバージョンの Windows が実行されている。
-   ホストとターゲットコンピューターは、カーネルデバッグ用に構成されています。 詳細については、「 [Visual Studio でのネットワーク接続の設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-in-visual-studio)」を参照してください。

**ハードウェア要件**

クライアントドライバーを書き込む USB デバイスを取得します。 ほとんどの場合、USB デバイスとそのハードウェア仕様が用意されています。 この仕様では、デバイスの機能とサポートされているベンダーのコマンドについて説明します。 仕様を使用して、USB ドライバーの機能と関連する設計上の決定を決定します。

USB ドライバーの開発を初めて行う場合は、OSR USB FX2 learning kit を使用して、WDK に含まれている USB サンプルを調査してください。 この学習キットは、 [OSR オンライン](https://www.osronline.com/)で入手できます。 このファイルには、USB FX2 デバイスと、クライアントドライバーを実装するために必要なすべてのハードウェア仕様が含まれています。

Microsoft USB Test Tool (MUTT) デバイスを取得することもできます。 MUTT ハードウェアは、 [Jjg テクノロジ](https://jjgtechnologies.com/mutt.md)から購入できます。 デバイスにインストールされているファームウェアがインストールされていません。 ファームウェアをインストールするには、[この Web サイト](https://msdn.microsoft.com/windows/hardware/jj590752)から MUTT ソフトウェアパッケージをダウンロードし、MUTTUtil を実行します。 詳細については、パッケージに含まれているドキュメントを参照してください。

**推奨資料**

-   [すべてのドライバー開発者向けの概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)
-   [デバイス ノードとデバイス スタック](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)
-   [Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index)
-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   *Windows Driver Foundation でのドライバーの開発*。これは、少額 Orwick と Guy Smith によって記述されています。 詳細については、「 [WDF を使用したドライバーの開発](https://msdn.microsoft.com/windows/hardware/gg463318)」を参照してください。

<a name="instructions"></a>手順
------------

### <a href="" id="generate-the-kmdf-driver-code-by-using-the--visual-studio-professional-2019---usb-driver-template"></a>手順 1: Visual Studio Professional 2019 USB ドライバーテンプレートを使用して KMDF ドライバーコードを生成する

KMDF ドライバーコードを生成する手順については、「[テンプレートに基づいて kmdf ドライバーを作成する](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-kmdf-driver-based-on-a-template)」の手順を参照してください。

**USB 固有のコードの場合は Visual Studio Professional 2019 で次のオプションを選択します。**

1.  [**新しいプロジェクト**] ダイアログボックスの上部にある [検索] ボックスに、「USB」と入力し**ます。**
2.  中央のウィンドウで、[**カーネルモードドライバー、USB (KMDF)**] を選択します。
3.  **[次へ]** をクリックします。
4.  プロジェクト名を入力し、保存場所を選択して、[**作成**] をクリックします。

次のスクリーンショットは、 **USB カーネルモードドライバー**テンプレートの [**新しいプロジェクト**] ダイアログボックスを示しています。

![visual studio の新しいプロジェクトオプション](images/kmdf-template-visual-studio-2019.png)

![visual studio の [新しいプロジェクト] オプション2番目の画面](images/kmdf-template-visual-studio-2019-2.png)

このトピックでは、Visual Studio プロジェクトの名前が "MyUSBDriver\_" であることを前提としています。 次のファイルが含まれています。

| ファイル                      | 説明                                                                                                          |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|
| パブリック .h                   | クライアントドライバーおよび USB デバイスと通信するユーザーアプリケーションによって共有される共通の宣言を提供します。 |
| *&lt;プロジェクト名&gt;*.inf | ターゲットコンピュータにクライアントドライバをインストールするために必要な情報が含まれています。                                   |
| トレース .h                    | トレース関数とマクロを宣言します。                                                                               |
| Driver. h;Driver .c         | ドライバーのエントリポイントとイベントコールバックルーチンを宣言して定義します。                                                |
| デバイス .h;Device. c         | ハードウェアの準備イベントのイベントコールバックルーチンを宣言して定義します。                                          |
| Queue. h;Queue .c           | フレームワークの queue オブジェクトによって発生するイベントのイベントコールバックルーチンを宣言して定義します。                 |

 

### <a href="" id="modify-the-inf-file-to-add-information-about-your-device"></a>手順 2: INF ファイルを変更してデバイスに関する情報を追加する

ドライバーをビルドする前に、デバイスに関する情報 (具体的にはハードウェア ID 文字列) を使用して、テンプレートの INF ファイルを変更する必要があります。

**ソリューションエクスプローラー**の [**ドライバーファイル**] で、INF ファイルをダブルクリックします。

INF ファイルでは、製造元、プロバイダー名、デバイスセットアップクラスなどの情報を指定できます。 提供する必要がある情報の1つは、デバイスのハードウェア識別子です。

ハードウェア ID 文字列を指定するには:

1.  USB デバイスをホストコンピューターに接続し、Windows によってデバイスが列挙されるようにします。
2.  **デバイスマネージャー**を開いて、デバイスのプロパティを開きます。
3.  [**詳細**] タブで、[プロパティ] の下にある [**ハードワード id** ] を選択し**ます。**

    デバイスのハードウェア ID がリストボックスに表示されます。 右クリックして、[ハードウェア ID] 文字列をコピーします。

4.  次の行にある USB\\VID\_vvvv & PID\_pppp を、ご使用のハードウェア ID 文字列に置き換えます。

    `[Standard.NT$ARCH$] %MyUSBDriver_.DeviceDesc%=MyUSBDriver__Device, USB\VID_vvvv&PID_pppp`

### <a href="" id="build-the-usb-client-driver-code"></a>手順 3: USB クライアントドライバーコードを作成する

**ドライバーをビルドするには**

1.  Visual Studio Professional 2019 でドライバープロジェクトまたはソリューションを開きます。
2.  **ソリューションエクスプローラー**でソリューションを右クリックし、[ **Configuration Manager**] を選択します。
3.  **Configuration Manager**で、**アクティブなソリューション構成**(たとえば、 **Windows 8 デバッグ**または**windows 8 Release**) と、対象のビルドの種類に対応する**アクティブなソリューションプラットフォーム**(Win32 など) を選択します。
4.  [**ビルド**] メニューの [**ソリューションのビルド**] をクリックします。

詳細については、「[ドライバーのビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)」を参照してください。

### <a href="" id="configure-a-computer-for-testing-and-debugging"></a>手順 4: テストおよびデバッグ用にコンピューターを構成する

ドライバーをテストしてデバッグするには、ホストコンピューター上でデバッガーを実行し、ターゲットコンピューターでドライバーを実行します。 ここまでで、ホストコンピューターで Visual Studio を使用してドライバーをビルドしました。 次に、対象のコンピューターを構成する必要があります。 ターゲットコンピューターを構成するには、「[ドライバーの展開およびテスト用のコンピューターのプロビジョニング](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の手順に従います。

### <a href="" id="enable-tracing-for-kernel-debugging"></a>手順 5: カーネルデバッグのトレースを有効にする

テンプレートコードには、関数呼び出しの追跡に役立つトレースメッセージ (TraceEvents) がいくつか含まれています。 ソースコード内のすべての関数には、ルーチンのエントリと終了をマークするトレースメッセージが含まれています。 エラーの場合、トレースメッセージにはエラーコードと意味のある文字列が含まれます。 ドライバープロジェクトでは、WPP トレースが有効になっているため、ビルド処理中に作成される PDB シンボルファイルには、トレースメッセージの書式設定命令が含まれます。 WPP トレース用にホストとターゲットコンピューターを構成した場合、ドライバーはトレースメッセージをファイルまたはデバッガーに送信できます。

**WPP トレース用にホストコンピューターを構成するには**

1. PDB シンボルファイルからトレースメッセージの書式設定命令を抽出して、トレースメッセージ形式 (TMF) ファイルを作成します。

   Tracepdb を使用して、TMF ファイルを作成できます。 このツールは、 <em>&lt;インストールフォルダー&gt;</em>Windows kit\\8.0\\bin\\*&lt;architecture&gt;* フォルダーにあります。 次のコマンドは、ドライバープロジェクト用の TMF ファイルを作成します。

   **tracepdb-f \[PDBFiles\]-p \[TMFDirectory\]**

   **-F**オプションは、PDB シンボルファイルの場所と名前を指定します。 **-P**オプションは、tracepdb によって作成される tmf ファイルの場所を指定します。 詳細については、「 [**Tracepdb コマンド**](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracepdb-commands)」を参照してください。

   指定した場所に、3つのファイルが表示されます (プロジェクトの c ファイルごとに1つ)。 GUID ファイル名が与えられます。

2. デバッガーで、次のコマンドを入力します。
   1.  **. load Wmitrace**

       Wmitrace 拡張子を読み込みます。

   2.  **. チェーン**

       デバッガー拡張機能が読み込まれていることを確認します。

   3.  **! wmitrace searchpath + * * *&lt;TMF ファイルの場所&gt;*

       TMF ファイルの場所をデバッガー拡張機能の検索パスに追加します。

       出力は次のようになります。

       `Trace Format search path is: 'C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE;c:\drivers\tmf'`

**WPP トレース用にターゲットコンピューターを構成するには**

1. ターゲットコンピューターに Tracelog ツールがインストールされていることを確認します。 このツールは、 <em>&lt;install\_フォルダー&gt;</em>Windows kit\\8.0\\Tools\\*&lt;arch&gt;* フォルダーにあります。 詳細については、「 [**Tracelog コマンドの構文**](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog-command-syntax)」を参照してください。
2. **コマンドウィンドウ**を開き、管理者として実行します。
3. 次のコマンドを入力します。

   **トレースログ-開始 mytrace-guid \#c918ee71-68c7-4140-8f7d-c907abbcb05d-フラグ 0xffff-level 7-rt-kd**

   このコマンドは、MyTrace という名前のトレースセッションを開始します。

   **Guid**引数は、クライアントドライバーであるトレースプロバイダーの guid を指定します。 Visual Studio Professional 2019 プロジェクトの resource.h から GUID を取得できます。 別のオプションとして、次のコマンドを入力し、guid ファイルに GUID を指定することもできます。 このファイルには、次のように、GUID がハイフン形式で含まれています。

   **トレースログ-開始 mytrace-guid c:\\drivers\\Provider. guid-flag 0xffff-level 7-rt-kd**

   次のコマンドを入力すると、トレースセッションを停止できます。

   **トレースログ-mytrace の停止**

### <a href="" id="deploy-the-driver-on-the-target-computer"></a>手順 6: ターゲットコンピューターにドライバーを展開する

1. [**ソリューションエクスプローラー** ] ウィンドウで、[ <em>&lt;プロジェクト名&gt;</em>**パッケージ**] を右クリックし、[**プロパティ**] を選択します。
2. 左側のウィンドウで、[**構成プロパティ] &gt; [ドライバー] [インストール &gt; の展開**] の順に移動します。
3. [展開の有効化] チェックボックスをオンにし、[ドライバーストアへのインポート] をオンにします。
4. [**リモートコンピューター名**] に、対象のコンピューターの名前を指定します。
5. **[Install and Verify (インストールと確認)]** を選びます。
6. **[OK]** をクリックします。
7. **[デバッグ]** メニューの **[デバッグ開始]** をクリックするか、キーボードで **F5** キーを押します。

**注**  **ハードウェア Id ドライバーの更新プログラム**では、デバイスのハードウェア id*を指定しないでください*。 ハードウェア ID は、ドライバーの情報 (INF) ファイルでのみ指定する必要があります。

 

Visual Studio Professional 2019 でターゲットシステムにドライバーを展開する方法の詳細については、「[テストコンピューターへのドライバーの展開](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

また、デバイスマネージャーを使用して、対象のコンピューターにドライバーを手動でインストールすることもできます。 コマンドプロンプトからドライバーをインストールする場合は、次のユーティリティを使用できます。

-   [PnPUtil](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil)

    このツールには、Windows が付属しています。 Windows\\System32 にあります。 このユーティリティを使用して、ドライバーをドライバーストアに追加することができます。

    ```cmd
    C:\>pnputil /a m:\MyDriver_.inf
    Microsoft PnP Utility

    Processing inf : MyDriver_.inf
    Driver package added successfully.
    Published name : oem22.inf
    ```

    詳細については、「 [PnPUtil の例](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil-examples)」を参照してください。

-   [**DevCon 更新プログラム**](https://docs.microsoft.com/windows-hardware/drivers/devtest/devcon-update)

    このツールには、WDK が付属しています。 ドライバーをインストールおよび更新するために使用できます。

    ```cmd
    devcon update c:\windows\inf\MyDriver_.inf USB\VID_0547&PID_1002\5&34B08D76&0&6
    ```

### <a href="" id="view-the-driver-in-device-manager"></a>手順 7: デバイスマネージャーでドライバーを表示する

1.  次のコマンドを入力して**デバイスマネージャー**を開きます。

    **devmgmt**

2.  **デバイスマネージャー**に次のノードのノードが表示されていることを確認します。

    **サンプル**

    **MyUSBDriver\_デバイス**

### <a href="" id="view-the-output-in-the-debugger"></a>手順 8: デバッガーで出力を表示する

Visual Studio では、最初に [**出力**] ウィンドウに進行状況が表示されます。 次に、デバッガーの [**イミディエイト] ウィンドウ**が開きます。 ホストコンピューターのデバッガーにトレースメッセージが表示されていることを確認します。 出力は次のようになります。 "MyUSBDriver\_" はドライバーモジュールの名前です。

```cpp
[3]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]MyUSBDriver_EvtDriverContextCleanup Entry
[1]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]MyUSBDriver_EvtDriverDeviceAdd Entry
[1]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]MyUSBDriver_EvtDriverDeviceAdd Exit
[0]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]DriverEntry Entry
[0]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]DriverEntry Exit
```

## <a name="related-topics"></a>関連トピック
[USB クライアントドライバーの KMDF テンプレートコードについて](understanding-the-kmdf-template-code-for-usb.md)  
[USB クライアント ドライバー開発の概要](getting-started-with-usb-client-driver-development.md)
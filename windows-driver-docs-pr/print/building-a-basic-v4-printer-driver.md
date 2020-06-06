---
title: 基本的な v4 プリンター ドライバーの構築
description: Microsoft Visual Studio 2017 のドライバ開発ウィザードを使用して、基本的な v4 プリンタドライバを構築し、機能するプリンタドライバを作成するための最小限の機能セットを選択します。
ms.assetid: 6E50CD69-D385-4724-B6B1-85D42EFFC6F0
ms.date: 02/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 83eb7759e9b3b77cb2efed684441daaf1789ff59
ms.sourcegitcommit: f0e54ea159d168a77643bf2e098d6b90e92b528c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455558"
---
# <a name="building-a-basic-v4-printer-driver"></a>基本的な v4 プリンター ドライバーの構築

Microsoft Visual Studio 2017 のドライバ開発ウィザードを使用して、基本的な v4 プリンタドライバを構築し、機能するプリンタドライバを作成するための最小限の機能セットを選択します。

このトピックの手順では、ドライバーを構築するために必要な手順に焦点を当てます。ウィザードで使用できる多くのプリンタードライバーオプションについては説明しません。 このトピックの目的は、Visual Studio 2017 でプリンタードライバーを開発するときのプロセスの概要を説明することです。 プリンタードライバーのオプションの詳細については、「[ウィザードのドライバーオプション](exploring-the-driver-options-in-the-wizard.md)について」を参照してください。

## <a name="instructions"></a>Instructions

### <a name="select-features-for-the-basic-driver"></a>基本ドライバーの機能を選択する

1. Visual Studio のメインメニューで、[**ファイル**] [  >  **新規作成**] [プロジェクト] の順にクリックし  >  **Project**ます。

2. [**新しいプロジェクト**] ウィンドウで、右上にある検索ボックスに「 *printer driver v4* 」と入力し、enter キーを押します。 これにより、名前に検索テキストが含まれているすべてのドライバーテンプレートが取得されます。

3. 中央のウィンドウで、[**プリンタードライバー V4**] を選択します。

4. [**名前**] フィールドにドライバーの名前を入力し、[ **OK**] をクリックします。 たとえば、「 *MyV4PrintDriver*」と入力します。

5. **V4 印刷ドライバーの作成ウィザード**の [**ドライバー表示の種類を選択**してください] で、[**カスタムレンダリングフィルター付き v4 印刷ドライバー (XPS のみを受け入れる)**] をクリックします。

6. その他のオプションはすべて既定の設定のままにして、[**次へ**] をクリックします。

7. ウィザードの [**セットアップ情報**] セクションで、すべてのオプションを既定の設定のままにして、[**次へ**] をクリックします。

8. ウィザードの [**セットアップ情報 (ページ 2)** ] セクションで、すべてのオプションを既定の設定のままにして、[**次へ**] をクリックします。

Microsoft Visual Studio では、前の選択項目を使用して*MyV4PrintDriver*のプロジェクトファイルが生成されます。

### <a name="verify-the-generated-driver-files"></a>生成されたドライバーファイルを確認する

1. 生成されたドライバーファイルのフォルダーに移動します。 たとえば、プロジェクトに*MyV4PrintDriver*という名前を付けた場合、既定では、ファイルは *[マイドキュメント] > Visual Studio 2017 > プロジェクト > MyV4PrintDriver > MyV4PrintDriver*に保存されます。

2. フォルダーに次のファイルが含まれていることを確認します。

    | ファイル名                                              | ファイルの種類                                                  |
    |--------------------------------------------------------|------------------------------------------------------------|
    | MyV4PrintDriver.gpd                                    | プリンターの説明ファイル                                   |
    | MyV4PrintDriver                                    | セットアップ情報ファイル                                     |
    | MyV4PrintDriver                                | C++ プロジェクトファイル                                           |
    | MyV4PrintDriver                        | C++ プロジェクトフィルターファイル                                   |
    | MyV4PrintDriver-manifest                           | 構成設定ファイル (別名 プリンタドライバマニフェスト) |
    | V4PrintDriver-Intellisense                          | Intellisense の JavaScript ファイル                           |
    | V4PrintDriver-Intellisense-Windows 8.1 js               | Intellisense の JavaScript ファイル                           |

上の表から、作成されたファイルの1つが INF ファイルであることがわかります。 Visual Studio では、ドライバーのインストールに使用できるように完了する必要があるスケルトンの INF ファイルが作成されていることに注意してください。

### <a name="create-a-unique-printerdriverid-for-the-driver"></a>ドライバーの一意の**プリンター Driverid**を作成します。

1. [Visual Studio Tools] メニューで [ **GUID の作成**] を選択します。

2. オプション4を選択し**ます。[レジストリ形式**] をクリックし、[**コピー** ] ボタンをクリックします。

3. Visual Studio のソリューションエクスプローラーで、[ *MyV4PrintDriver* ] ノードを展開します。

4. [**ドライバーファイル**] をクリックし、[**プロパティ**] ウィンドウで、[*一意の識別子*] フィールドの値を確認します。 この値は、**貼り付け**を使用して生成した GUID に置き換えます。

### <a name="complete-the-inf-file"></a>INF ファイルの完成

MyV4PrintDriver プロジェクトでは、**ドライバーファイル**のエントリが存在する必要があります。 これを開くと、MyV4PrintDriver ファイルが表示されます。 このファイルを開きます。

#### <a name="1-update-the-copyright-notice"></a>1. 著作権表示を更新する

INF ファイルの最初の2行は、ドライバーパッケージの著作権に関する声明です。

1行目には、会社の年と名前が含まれています。 YYYY の文字を現在の年に置き換え、製造元の>*名前*<文字を会社の名前に置き換えます。

2行目では、製造元の名前とデバイスのモデル情報を含むドライバー INF の内容について説明します。 *製造元の名前*<文字> 会社の名前に置き換え、<*プリンター> モデル*の文字を、ドライバーでサポートされているプリンターのモデル名に置き換えます。

たとえば、年が2017で、会社の名前が Fabrikam で、印刷デバイスモデルが1234の場合、次のように入力します。

```inf
; Copyright (c) 2017 Fabrikam
; INF file for the Fabrikam 1234 print driver
```

#### <a name="2-verify-the-version-section-is-correct"></a>2. ** \[ バージョン \] **セクションが正しいことを確認します。

** \[ バージョン \] **を含む行を探します。

- 次の行が表示されていることを確認します。

    ```inf
    **ClassVer**=4.0
    ```

- 次の行が表示されていることを確認します。

    ```inf
    **Signature**="$WINDOWS NT$"
    ```

#### <a name="3-configure-the-sourcedisksfiles-section"></a>3. ** \[ sourcedisksfiles \] **セクションを構成する

** \[ Sourcedisksfiles \] **を含む行を探します。

この型の下に次の行を入力します。

```inf
MyV4PrintDriver.gpd=1
MyV4PrintDriver-manifest.ini=1
MyV4PrintDriverRenderFilter-PipelineConfig.xml=1
MyV4PrintDriverRenderFilter.dll=1
```

#### <a name="4-configure-the-driverfiles-section"></a>4. ** \[ driverfiles \] **セクションを構成する

** \[ Driverfiles \] **を含む行を探します。

この型の下に次の行を入力します。

```inf
MyV4PrintDriver.gpd
MyV4PrintDriver-manifest.ini
MyV4PrintDriverRenderFilter-PipelineConfig.xml
MyV4PrintDriverRenderFilter.dll
```

#### <a name="5-configure-the-standardntarch-section"></a>5. ** \[ STANDARD. NT $ ARCH $ \] **セクションを構成する

** \[ 標準の NT $ ARCH $ \] **を含む行を探します。

このセクションでは、各モデルの INF のインストールセクションを参照します。 たとえば、プリンターのモデルが Fabrikam 1234 の場合、次のように入力します。

```inf
"Fabrikam 1234"=DriverInstall, USBPRINT\\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\\Fabrikam1234
```

#### <a name="6-add-printerdriverid-to-the-inf-file"></a>6.**プリンター Driverid**を INF ファイルに追加する

Visual Studio のソリューションエクスプローラーで、[ *MyV4PrintDriver* ] ノードを展開します。

[**ドライバーファイル**] をクリックし、[**プロパティ**] ウィンドウで、[*一意識別子*] フィールドの値を確認します。 これは、ドライバー ID (GUID) です。 強調表示してコピーする

INF ファイルの、 ** \[ STANDARD. NT $ ARCH $ \] **セクションに、次の行を入力します。

```inf
"Fabrikam 1234"=DriverInstall,
```

コンマの後に、前の手順でコピーした GUID を貼り付けます。 完成した** \[ 標準の NT $ ARCH \] $** セクションは、次のようになります。

```inf
"Fabrikam 1234"=DriverInstall, {GUID}
"Fabrikam 1234"=DriverInstall, USBPRINT\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\Fabrikam1234
```

#### <a name="7-configure-the-strings-section"></a>7. ** \[ Strings \] **セクションを構成する

** \[ 文字列 \] **を含む行を検索します。

ここでは、 *ManufacturerName*文字列の定義を確認します。 製造元の>*名前*<文字を会社の名前に置き換えて、ターゲットプリンターの製造元の名前を指定し、を含むその他の行を削除します。法

たとえば、会社の名前が Fabrikam の場合、次のように入力します。

```inf
ManufacturerName="Fabrikam"
```

#### <a name="8-save-the-inf-file"></a>8. INF ファイルを保存する

INF ファイルが完成すると、次のようになります。

```inf
; Copyright (c) 2017 Fabrikam
; INF file for the Fabrikam 1234 print driver

[Version]
Signature="$Windows NT$"
Class=Printer
ClassGuid={4D36E979-E325-11CE-BFC1-08002BE10318}
Provider=%ManufacturerName%
CatalogFile=MyV4PrintDriver.cat
ClassVer=4.0
DriverVer=03/17/2014,1.0.0.0

[Manufacturer]
%ManufacturerName%=Standard,NT$ARCH$

[Standard.NT$ARCH$]
"Fabrikam 1234"=DriverInstall, {GUID}
"Fabrikam 1234"=DriverInstall, USBPRINT\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\Fabrikam1234

[DriverInstall]
CopyFiles=DriverFiles

[DriverFiles]
MyV4PrintDriver.gpd
MyV4PrintDriver-manifest.ini
MyV4PrintDriverRenderFilter-PipelineConfig.xml
MyV4PrintDriverRenderFilter.dll

[DestinationDirs]
DefaultDestDir = 66000

[SourceDisksNames]
1 = %DiskName%,,,""

[SourceDisksFiles]
MyV4PrintDriver.gpd=1
MyV4PrintDriver-manifest.ini=1
MyV4PrintDriverRenderFilter-PipelineConfig.xml=1
MyV4PrintDriverRenderFilter.dll=1

[Strings]
ManufacturerName="Fabrikam"
DiskName="MyV4PrintDriver Installation Disk"
```

### <a name="update-the-driver-files-list"></a>**ドライバーファイル**の一覧を更新する

1. Visual Studio のソリューションエクスプローラーで、[ *MyV4PrinterDriver* ] ノードを展開します。

2. MyV4PrintDriver ファイルを選択し、[**ドライバーファイル**] ノードにドラッグします。

3. MyV4PrintDriver-manifest と同じ操作を行います。

### <a name="add-the-pipeline-config-file-to-the-driver-package"></a>パイプライン構成ファイルをドライバーパッケージに追加する

1. ソリューションエクスプローラーで、[ *MyV4PrintDriver* project] を右クリックし、[**プロパティ**] をクリックします。

2. MyV4PrintDriver の [**プロパティページ**] ウィンドウで、左ペインの [**構成プロパティ**] を展開します。

3. [**ドライバーのインストール**] を展開し、[**パッケージファイル**] をクリックします。 右側のウィンドウで、次の操作を行います。
    - プロジェクトディレクトリに移動します。
    - *MyV4PrintDriver Render Filter*ディレクトリに移動します。
    - MyV4PrintDriverRenderFilter-PipelineConfig ファイルを選択し、[**開く**] をクリックします。
    - [**OK**] をクリックします。

### <a name="add-a-reference-to-the-render-filter-to-the-driver-package"></a>ドライバーパッケージにレンダーフィルターへの参照を追加する

1. Visual Studio のソリューションエクスプローラーで、[ *MyV4PrinterDriver* ] ノードを展開します。

2. [**参照**] ノードを右クリックし、[**参照の追加**] を選択し > ます。

3. [ *MyV4PrintDriver Render Filter*] のチェックボックスをオンにし、[ **OK**] をクリックします。

### <a name="configure-the-driver-solution-for-debugging-and-deployment"></a>デバッグと配置のためにドライバーソリューションを構成する

1. ソリューションエクスプローラーで、[ *MyV4PrintDriver* project] を右クリックし、[**プロパティ**] をクリックします。

2. MyV4PrintDriver の [**プロパティページ**] ウィンドウで、左ペインの [**構成プロパティ**] を展開します。

3. [**ドライバーのインストール**] を展開し、[**展開**] をクリックします。 右側のウィンドウで、次の操作を行います。
    - **ターゲットコンピューター名**が構成されていることを確認します。 そうでない場合は、[...] をクリックします。**デバイスの構成**ウィザードの指示に従って、リモートのターゲットコンピューターを設定します。
    - **[展開前にドライバーの以前のバージョンを削除する]** チェック ボックスをオンにします。
    - [**インストール/再インストールと確認**] を選択し、ドロップダウンボックスから [**既定のプリンタードライバーパッケージのインストールタスク**] を選択します。
    - [**オプションの引数**] フィールドにドライバーの名前を入力します (名前は引用符で囲まないでください)。
    - [**OK**] をクリックします。

### <a name="configure-driver-signing"></a>ドライバー署名の構成

1. ソリューションエクスプローラーで、[ *MyV4PrintDriver* project] を右クリックし、[**プロパティ**] をクリックします。

2. MyV4PrintDriver の [**プロパティページ**] ウィンドウで、左ペインの [**構成プロパティ**] を展開します。

3. [**ドライバーの署名**] を展開し、[**全般**] をクリックします。

4. 右側のウィンドウで、[ **Sign Mode** ] が [Test sign] に設定されていることを確認します。

5. [**テスト証明書**] をクリックし、ドロップダウンボックスから [**テスト証明書の作成...** ] を選択します。

6. [タイム**スタンプサーバー**] をクリックし、ドロップダウンボックスから [Verisign] を選択します。

7. [**OK**] をクリックします。

### <a name="build-and-deploy-the-driver"></a>ドライバーをビルドして展開する

1. ソリューションエクスプローラーで、[ *Solution MyV4PrintDriver (2 プロジェクト)*] を右クリックし、[**ソリューションのビルド**] をクリックします。

2. ビルドプロセスが完了すると、ドライバーが自動的にインストールされます。 [出力] ウィンドウにエラーがないことを確認します。

### <a name="test-the-driver"></a>ドライバーをテストする

プラグアンドプレイまたはプリンターの追加ウィザードを使用して、印刷キューを作成します。

V4 プリンタードライバーの INF ファイルの詳細については、「 [V4 ドライバー inf](v4-driver-inf.md)」を参照してください。

> [!NOTE]
> 前の表のファイルに加えて、 *MyV4PrintDriver Render Filter*フォルダーが作成されていることに注意してください。 これはレンダーフィルタープロジェクトテンプレートであり、XPS レンダリングフィルターおよび XPS フィルターパイプライン構成ファイルを構築するための優れた基盤となります。 XPS レンダリングフィルターの詳細については、「 [XPSDrv Render Module](xpsdrv-render-module.md)」を参照してください。 xps レンダリングフィルターの例については、 [Xps ラスタライズフィルターサービス](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/xps-rasterization-filter-service-sample/)のサンプルを参照してください。

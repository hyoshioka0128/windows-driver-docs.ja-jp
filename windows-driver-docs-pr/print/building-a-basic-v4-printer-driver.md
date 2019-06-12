---
title: 基本的な v4 プリンター ドライバーの構築
description: 機能のプリンター ドライバーを作成する機能の最小セットを選択して、Microsoft Visual Studio 2017 でドライバー開発ウィザードを使用して基本的な v4 プリンター ドライバーをビルドします。
ms.assetid: 6E50CD69-D385-4724-B6B1-85D42EFFC6F0
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 03e4f77618193c0778250e3a623f34899e3cac1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330413"
---
# <a name="building-a-basic-v4-printer-driver"></a>基本的な v4 プリンター ドライバーの構築

機能のプリンター ドライバーを作成する機能の最小セットを選択して、Microsoft Visual Studio 2017 でドライバー開発ウィザードを使用して基本的な v4 プリンター ドライバーをビルドします。

このトピックの手順は、ドライバーを構築するために必要な手順に焦点し、ウィザードで使用できる多くのプリンター ドライバー オプションについては説明しません。 このトピックの目的は、Visual Studio 2017 でのプリンター ドライバーを開発するときに、関連するプロセスの概要を提供します。 プリンター ドライバーのオプションの詳細についてで提供される[ウィザードでドライバーのオプションを探索](exploring-the-driver-options-in-the-wizard.md)します。

## <a name="instructions"></a>手順

### <a name="select-features-for-the-basic-driver"></a>基本的なドライバーの機能を選択します。

1. Visual Studio で、メインのメニューでクリックして**ファイル** &gt; **新規** &gt; **プロジェクト**します。

2. **新しいプロジェクト**ウィンドウで、右上の検索ボックスに「*プリンター ドライバー v4*し、enter キーを押します。 名前に、検索テキストを含むすべてのドライバー テンプレートが取得されます。

3. 中央のペインで選択**プリンター ドライバー V4**します。

4. ドライバーの名前を入力、**名前**フィールドをクリックして**OK**します。 たとえば、入力する*MyV4PrintDriver*します。

5. **V4 印刷ドライバー ウィザードを作成する**[**ドライバーの表示の種類を選択:** 、] をクリックして**カスタム レンダリング フィルターを使用した V4 印刷ドライバー (だけ XPS を受け入れる)** します。

6. その他のすべてのオプションのままにして、既定の設定とクリックして**次**します。

7. **セットアップ情報**セクションと、ウィザードのすべてのオプションのままにして、既定の設定 をクリックし、**次**します。

8. **セットアップ情報 (ページ 2)** セクションと、ウィザードのすべてのオプションのままにして、既定の設定 をクリックし、**次**します。

Microsoft Visual Studio は、前の選択を使用してプロジェクト ファイルを生成する*MyV4PrintDriver*します。

### <a name="verify-the-generated-driver-files"></a>生成されたドライバー ファイルを確認します。

1. 生成されたドライバー ファイルのフォルダーに移動します。 たとえば、プロジェクトの名前を付けた*MyV4PrintDriver*既定では、次の場所にファイルを保存は。*マイ ドキュメント&gt;Visual Studio 2017&gt;プロジェクト&gt;MyV4PrintDriver &gt; MyV4PrintDriver*します。

2. フォルダーに、次のファイルが含まれていることを確認します。

    | ファイル名                                              | ファイルの種類                                                  |
    |--------------------------------------------------------|------------------------------------------------------------|
    | MyV4PrintDriver.gpd                                    | プリンターの記述ファイル                                   |
    | MyV4PrintDriver.inf                                    | セットアップ情報ファイル                                     |
    | MyV4PrintDriver.vcxproj                                | C++ プロジェクト ファイル                                           |
    | MyV4PrintDriver.vcxproj.filters                        | C++ のプロジェクト フィルター ファイル                                   |
    | MyV4PrintDriver-manifest.ini                           | 構成設定ファイル (別名。 印刷ドライバー マニフェスト) |
    | V4PrintDriver-Intellisense.js                          | Intellisense の JavaScript ファイル                           |
    | V4PrintDriver-Intellisense-Windows8.1.js               | Intellisense の JavaScript ファイル                           |

作成されるファイルの 1 つ前の表からの通知は、INF ファイルです。 Visual Studio ができるため、ドライバーをインストールするために使用できますが、スケルトン INF ファイルを作成することに注意してください。

### <a name="create-a-unique-printerdriverid-for-the-driver"></a>一意な作成**PrinterDriverID**ドライバー

1. Visual Studio ツール メニューで選択**GUID の作成**です。

2. オプションを選択**4。レジストリ形式** をクリックし、**コピー**ボタンをクリックします。

3. ソリューション エクスプ ローラーで、Visual Studio で、展開、 *MyV4PrintDriver*ノード。

4. をクリックして**ドライバー ファイル**、次に、**プロパティ**ウィンドウの値を見て、*一意識別子*フィールド。 この値を使用して生成した GUID に置き換えます**貼り付け**します。

### <a name="complete-the-inf-file"></a>INF ファイルを完了します。

MyV4PrintDriver プロジェクトはエントリ**ドライバー ファイル**します。 これと MyV4PrintDriver.inf が表示されるはずのファイルを開きます。 このファイルを開きます。

#### <a name="1-update-the-copyright-notice"></a>1. 著作権情報を更新します。

INF ファイルの最初の 2 行は、ドライバー パッケージの著作権の通知です。

1 行目には、会社の名前と年が含まれています。 文字 YYYY は現在の年を置き換えるし、文字を置換<Your manufacturer name>会社の名前に置き換えます。

2 行目では、製造元名とデバイス モデルの情報を含むドライバーの INF の内容について説明します。 文字を置き換える&lt;製造元名&gt;、会社の名前の文字で置き換えると&lt;プリンター モデル&gt;ドライバーでサポートされているプリンターのモデルの名前に置き換えます。

たとえば場合は、会社の名前は、Fabrikam と印刷デバイス モデルは 1234 年は、2017、次のように入力します。

```cpp
; Copyright (c) 2017 Fabrikam
; INF file for the Fabrikam 1234 print driver
```

#### <a name="2-verfy-the-version-section-is-correct"></a>2. Verfy、 **\[バージョン\]** セクションが正しい

検索含む行 **\[バージョン\]** します。

- 確認し、この行が表示されるかどうかを確認します。

    ```cpp
    **ClassVer**=4.0
    ```
- 確認し、この行が表示されるかどうかを確認します。

    ```cpp
    **Signature**="$WINDOWS NT$"
    ```

#### <a name="3-configure-the-sourcediskfiles-section"></a>3.構成、 **\[SourceDiskFiles\]** セクション

検索含む行 **\[SourceDiskFiles\]** します。

その下には、次の行を入力します。

```cpp
MyV4PrintDriver.gpd=1
MyV4PrintDriver-manifest.ini=1
MyV4PrintDriverRenderFilter-PipelineConfig.xml=1
MyV4PrintDriverRenderFilter.dll=1
```

#### <a name="4-configure-the-driverfiles-section"></a>4。構成、 **\[DriverFiles\]** セクション

検索含む行 **\[DriverFiles\]** します。

その下には、次の行を入力します。

```cpp
MyV4PrintDriver.gpd
MyV4PrintDriver-manifest.ini
MyV4PrintDriverRenderFilter-PipelineConfig.xml
MyV4PrintDriverRenderFilter.dll
```

#### <a name="5-configure-the-standardntarch-section"></a>5。構成、 **\[Standard.NT$ARCH$\]** セクション

検索含む行 **\[Standard.NT$ARCH$\]** します。

このセクションでは、各モデルの INF のインストール」セクションを参照します。 たとえば、プリンターのモデルが Fabrikam 1234 の場合は、しを入力次します。

```cpp
"Fabrikam 1234"=DriverInstall, USBPRINT\\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\\Fabrikam1234
```

#### <a name="6-add-printerdriverid-to-the-inf-file"></a>6。追加**PrinterDriverID** INF ファイル

ソリューション エクスプ ローラーで、Visual Studio で、展開、 *MyV4PrintDriver*ノード。

クリックして**ドライバー ファイル**、次に、**プロパティ**ウィンドウの値を見て、*一意識別子*フィールド。 ドライバー ID (GUID) です。 強調表示し、それをコピー

INF ファイルでの **\[Standard.NT$ARCH$\]** セクションで、次の行を入力します。

```cpp
"Fabrikam 1234"=DriverInstall,
```

コンマの後に、前の手順でコピーした GUID を貼り付けます。 完成した **\[Standard.NT$ARCH$\]** セクションに次のようになります。

```cpp
"Fabrikam 1234"=DriverInstall, {GUID}
"Fabrikam 1234"=DriverInstall, USBPRINT\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\Fabrikam1234
```

#### <a name="7-configure-the-strings-section"></a>7.構成、 **\[文字列\]** セクション

検索含む行 **\[文字列\]** します。

その下の定義が表示されます、 *%manufacturername*文字列。 文字を置き換える&lt;製造元名&gt;ターゲットのプリンタの製造元の名を入力し、含んでいる行の残りの部分を削除、会社の名前を持つ、;TODO:

など、社名が Fabrikam である場合は、次のように入力します。

```cpp
ManufacturerName="Fabrikam"
```

#### <a name="8-save-the-inf-file"></a>8.INF ファイルを保存します。

INF ファイルを完了すると、次のようになります。

```cpp
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

### <a name="update-the-driver-files-list"></a>更新プログラム、**ドライバー ファイル**一覧

1. ソリューション エクスプ ローラーで、Visual Studio で、展開、 *MyV4PrinterDriver*ノード。

2. MyV4PrintDriver.gpd ファイルを選択し、ドラッグ、**ドライバー ファイル**ノード。

3. MyV4PrintDriver manifest.ini で同じ操作を行います。

### <a name="add-the-pipeline-config-file-to-the-driver-package"></a>ドライバー パッケージに、パイプラインの構成ファイルを追加します。

1. ソリューション エクスプ ローラーで右クリックして*MyV4PrintDriver*プロジェクトの **プロパティ**します。

2. **MyV4PrintDriver プロパティ ページ**ウィンドウで、展開**構成プロパティ**左側のウィンドウでします。

3. 展開**ドライバー インストール**、 をクリックし、**パッケージ ファイル**。 右側のウィンドウで、次の操作を行います。
    - プロジェクト ディレクトリに移動します。
    - 内に移動して、 *MyV4PrintDriver 表示フィルター*ディレクトリ。
    - ファイル MyV4PrintDriverRenderFilter PipelineConfig.xml とキーを押して選択**オープン**します。
    - **[OK]** をクリックします。

### <a name="add-a-reference-to-the-render-filter-to-the-driver-package"></a>ドライバー パッケージにレンダー フィルターへの参照を追加します。 

1. ソリューション エクスプ ローラーで、Visual Studio で、展開、 *MyV4PrinterDriver*ノード。

2. 右クリックして、**参照**ノードを選択]-> [**参照の追加**します。

3. チェック ボックスをクリックします。 *MyV4PrintDriver 表示フィルター*、順にクリックします**OK**します。

### <a name="configure-the-driver-solution-for-debugging-and-deployment"></a>デバッグと配置のドライバー ソリューションを構成します。

1. ソリューション エクスプ ローラーで右クリックして*MyV4PrintDriver*プロジェクトの **プロパティ**します。

2. **MyV4PrintDriver プロパティ ページ**ウィンドウで、展開**構成プロパティ**左側のウィンドウでします。

3. 展開**ドライバーのインストール**、 をクリックし、**展開**します。 右側のウィンドウで、次の操作を行います。
    - いることを確認、**ターゲット コンピューター名**が構成されています。 いない場合は、「...」 をクリックします。画面の指示に従って、**デバイスの構成**リモート ターゲット コンピューターを設定するウィザード。
    - **[展開前にドライバーの以前のバージョンを削除する]** チェック ボックスをオンにします。
    - 選択**インストール/再インストールと検証**を選択し、**プリンター ドライバー パッケージのインストールのタスクを既定の**ドロップダウン ボックスから。
    - 内のドライバーの名前を入力、**省略可能な引数**フィールド名を囲む引用符はすべて) (なし。
    - **[OK]** をクリックします。

### <a name="configure-driver-signing"></a>ドライバーの署名を構成します。

1. ソリューション エクスプ ローラーで右クリックして*MyV4PrintDriver*プロジェクトの **プロパティ**します。

2. **MyV4PrintDriver プロパティ ページ**ウィンドウで、展開**構成プロパティ**左側のウィンドウでします。

3. 展開**ドライバーの署名**、 をクリックし、**全般**します。

4. 右側のウィンドウで確認する**記号モード**テスト サインオンに設定されています。

5. クリックして**テスト証明書**を選択し、&lt;テスト証明書を作成しています.&gt;ドロップダウン ボックスから。

6. クリックして**TimeStampServer**、ドロップ ダウン ボックスから Verisign を選択します。

7. **[OK]** をクリックします。

### <a name="build-and-deploy-the-driver"></a>ドライバーをビルドして展開する

1. ソリューション エクスプ ローラーで右クリックして*ソリューション MyV4PrintDriver (2 プロジェクト)* 、 をクリック**ソリューションのビルド**します。

2. ビルド プロセスが完了すると、ドライバーが自動的にインストールされます。 出力ウィンドウにエラーがないことを確認します。

### <a name="test-the-driver"></a>ドライバーをテストします。

プラグ アンド プレイまたはプリンターの追加ウィザードを使用して印刷キューを作成します。

V4 プリンター ドライバーの INF ファイルの詳細については、次を参照してください。 [V4 ドライバーの INF](v4-driver-inf.md)します。

> [!NOTE]
> 上記の表に、ファイルだけでなくことに注意して、 *MyV4PrintDriver 表示フィルター*フォルダーが作成されました。 これは、レンダリングのフィルターのプロジェクト テンプレートと XPS の表示フィルターと XPS フィルター パイプライン構成ファイルを構築するための優れた基盤を提供します。 XPS 表示フィルターの詳細については、次を参照してください。 [XPSDrv レンダリング モジュール](xpsdrv-render-module.md)、XPS の表示フィルターの例を確認するには、参照してください、 [XPS ラスタライズ フィルター サービス](https://go.microsoft.com/fwlink/p/?LinkId=617951)サンプル。





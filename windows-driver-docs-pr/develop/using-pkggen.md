---
title: Windows 10 Mobile へのドライバーのインストール
description: Windows 10 Mobile へのドライバーのインストールについて説明します。
ms.date: 06/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34d19520e79745f3f0833010abac96767709dae9
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364185"
---
# <a name="installing-a-driver-on-windows-10-mobile"></a>Windows 10 Mobile へのドライバーのインストール

Windows 10 Mobile にドライバーをインストールするには、.spkg ファイルを使います。 .spkg ("*パッケージ ファイル*") は、ドライバー パッケージを含むスタンドアロン モジュールです。

WDK 10 には、パッケージ ファイルを生成する PkgGen というツールが付属しています。 ドライバーをビルドする場合は、次の手順に従って Visual Studio で PkgGen を実行します。

**PkgGen を使用したパッケージ ファイルの生成**

1.  ドライバー プロジェクトを右クリックし、 **[追加] &gt; [新しい項目]** の順に選びます。 次に、 **[Visual C++] &gt; [Windows Driver (Windows ドライバー)]** で、 **[パッケージ マニフェスト]** を選びます。 **[追加]** をクリックします。
2.  ドライバー プロジェクトに Package.pkg.xml という名前のファイルが追加されます。 ファイルを右クリックしてプロパティを選択すると、項目の種類が **PkgGen** であることを確認できます (このプロパティ ページで **ビルドから除外]** [ を ] **[はい** に設定すると、後でこのドライバー プロジェクトをビルドするときにパッケージ ファイルを生成しないようにすることができます)。 **[OK]** をクリックします。
3.  ドライバー プロジェクトを右クリックし、 **[プロパティ]** をクリックします。 [構成プロパティ] で、PackageGen ノードを開き、[バージョン] を任意のバージョンに変更します。
4.  作業内容を保存し、管理者として Visual Studio を再起動します。
5.  ドライバーをビルドします。 必要なライブラリがリンクされ、.cat ファイル、.inf ファイル、ドライバーのバイナリ、および .spkg ファイルが生成されます。

パッケージ ファイルの内容を確認するには、ファイル名に .cab というサフィックスを追加して、その cab ファイルをエクスプローラーで開きます。

Visual Studio の外部での PkgGen の実行については、「[モバイル パッケージの作成](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))」をご覧ください。

モバイル ドライバー パッケージ (.spkg ファイル) をインストールするには、2 つのオプションがあります。

-   ターゲット システムの既存のパッケージを更新する場合、または新しいパッケージをターゲットに追加する場合は、IUTool.exe を使用して、.spkg ドライバー パッケージをインストールします。
-   モバイル OS イメージにパッケージを組み合わせる場合は、ImgGen を使用して、Full Flash Update (FFU) イメージに .spkg ドライバー パッケージを追加し、モバイル デバイスにフラッシュできるようにします。

**IUTool を使用した、モバイル ドライバー パッケージ (.spkg) の実行中のデバイスへの追加**

1.  IUTool.exe は、WDK 10 の \\tools\\bin\\&lt;*アーキテクチャ*&gt; サブディレクトリにあります。

    モバイル デバイスを PC に接続します。 その後、管理者特権のコマンド プロンプトで次のコマンドを実行します。

       ```cpp
       IUTool -p MyKmdfDriver.spkg
       ```

2.  詳しくは、「[テスト イメージへのドライバーの追加](https://docs.microsoft.com/previous-versions/mt131832(v=vs.85))」をご覧ください。

**ImgGen を使用した、ドライバー パッケージ (.spkg) のモバイル OS イメージ (.ffu) への追加**

1.  Visual Studio をインストールしたら、スタート画面で [Visual Studio 2015] フォルダーをクリックします。 **[開発者コマンド プロンプト for VS2015]** を右クリックし、 **[管理者として実行]** を選びます。

## <a name="span-idflashing_a_mobile_os_image__ffu_spanspan-idflashing_a_mobile_os_image__ffu_spanflashing-a-mobile-os-image-ffu"></a><span id="flashing_a_mobile_os_image__.ffu_"></span><span id="FLASHING_A_MOBILE_OS_IMAGE__.FFU_"></span>モバイル OS イメージ (.ffu) のフラッシュ

デバイスにイメージをフラッシュするには、Microsoft から提供された FFUTool を使うか、カスタム OEM フラッシュ ツールを開発します。

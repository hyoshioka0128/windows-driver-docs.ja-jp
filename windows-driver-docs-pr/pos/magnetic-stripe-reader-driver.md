---
title: 磁気ストライプ リーダー ドライバーのサンプル
description: このサンプルでは、磁気ストライプリーダー用のユニバーサルドライバーを作成し、新しいドライバーを作成するためのテンプレートとして使用する方法を示します。
ms.assetid: 92A8C116-F71F-4A74-A453-44C14297BCDD
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 10f98a52fc904c8a5fc9329d4e3b63458673e4b0
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223527"
---
# <a name="magnetic-stripe-reader-driver-sample"></a>磁気ストライプ リーダー ドライバーのサンプル

磁気ストライプリーダードライバーのサンプルは、磁気ストライプリーダー用のユニバーサルドライバーを作成する方法を示しています。これは、新しいドライバーを作成するためのテンプレートとして使用することを目的としています。 このサンプルでは、ユーザーモードドライバーフレームワーク (UMDF) 2.0 を使用して、デバイスに排他アクセスを要求するなどの基本的な機能を示します。 このサンプルドライバーは、x86、amd64、および ARM の各プラットフォームでコンパイルして展開できます。

## <a name="requirements"></a>要件

- Windows 10

- [Microsoft Visual Studio](https://visualstudio.microsoft.com) (すべてのバージョン)

- [Windows Driver Kit (WDK) 10](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

Windows Software Development Kit (SDK) 10 も必要ですが、これは Microsoft Visual Studio の一部としてインストールされます。

> [!NOTE]
> サンプルドライバーは、ソフトウェアデバイスで動作するため、磁気ストライプリーダーハードウェアを機能させる必要はありません。 サンプルで使用するハードウェアデバイスがある場合でも、デバイスのハードウェア ID を INF ファイルに追加することによってドライバーを使用できます。

## <a name="download-and-extract-the-sample"></a>サンプルをダウンロードして抽出する

[Windows ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples)は、GitHub から入手できます。

1. [**Windows-driver-samples-master**](https://github.com/microsoft/Windows-driver-samples/archive/master.zip)をダウンロードします。 このファイルには、すべての Windows Driver Kit (WDK) のサンプルが含まれています。

1. 開発用コンピューター上の任意の場所に**Windows-driver-samples-master**を抽出します。 この `<sample_root>` 記事の残りの部分では、この場所をと呼びます。

## <a name="open-the-driver-solution-in-visual-studio"></a>Visual Studio でドライバーソリューションを開く

1. Windows エクスプローラーで、フォルダーに移動 `<sample_root>\pos\drivers\MagneticStripeReader` します。

1. ソリューションファイル**MagneticStripeReader**をダブルクリックして、Visual Studio でソリューションを開きます。

1. プロジェクトの zip ファイルがインターネットからダウンロードされたため、ソリューションを開いたときにセキュリティの警告が表示されることがあります。 その場合は、[ **OK** ] をクリックしてプロジェクトの読み込みを完了します。

1. Visual Studio で、**ソリューションエクスプローラー**を見つけます。 まだ開いていない場合は、[**表示**] メニューの [**ソリューションエクスプローラー** ] を選択します。 **ソリューションエクスプローラー**には、プロジェクトとそれに含まれるソースファイルが表示されます。

## <a name="build-the-sample-using-visual-studio"></a>Visual Studio を使用してサンプルをビルドする

1. Visual Studio の [*標準*] ツールバーで、使用しているオペレーティングシステムプラットフォームに合った*ソリューションプラットフォーム*を選択します。 たとえば、64ビット版の Windows を使用している場合は、[x64] を選択します。

    > [!NOTE]
    > ARM プラットフォームを対象とする場合は、構成マネージャーを使用してターゲットの一覧に ARM を追加する必要があります。

1. [**ビルド**] メニューの [**ソリューションのビルド**] を選択します。

## <a name="install-the-driver"></a>ドライバーのインストール

1. ビルドされると、ドライバーはテスト証明書で署名されています。 テスト用のドライバーをインストールするには、テスト証明書で署名されたドライバーが読み込むことができるように、ブート構成を変更する必要があります。 設定を変更するには、管理者特権でのコマンドプロンプトを開き、次のコマンドを入力します。

    `bcdedit.exe /set TESTSIGNING on`

1. コンピューターを再起動します。

    > [!NOTE]
    > テスト署名が既に有効になっている場合は、再起動は必要ありません。

1. 管理者特権でのコマンドプロンプトで、プロジェクトがビルドされたフォルダーに移動します。 X64 デバッグビルドを作成した場合、このフォルダーはになり `<project_root>\x64\Debug\SampleMagneticStripeReaderDrv` ます。

    このフォルダーには、次のファイルが表示されます。

    | ファイル                              | 説明                                                                  |
    |-----------------------------------|------------------------------------------------------------------------------|
    | SampleMagneticStripeReaderDrv | ドライバーファイル。                                                             |
    | SampleMagneticStripeReaderDrv | ドライバーのインストールに必要な情報が含まれている INF ファイル。          |
    | samplemagneticstripereaderdrv.cat | パッケージ全体の署名として機能する、署名されたカタログファイル。 |

1. OS とドライバーのプラットフォームに一致するデバイスコンソールユーティリティ (devcon) へのパスを特定します。 X64 バージョンの既定の場所は `C:\Program Files (x86)\Windows Kits\10\Tools\x64` です。

1. 次のコマンドを入力し &lt; ます。ここで、devcon \_ path &gt; は、前の手順で見つけた devcon ファイルへのパスに置き換えます。

    `"<devcon_path>\devcon.exe" install SampleMagneticStripeReaderDrv.inf Root\SampleMagneticStripeReaderDrv`

1. ドライバーの発行者を確認できないことを通知する**Windows セキュリティ**ダイアログが表示されます。 これは、ドライバーがテスト証明書で署名されたためです。 [**このドライバソフトウェアをインストール**する] をクリックします。 この時点で、ドライバーが正しくインストールされたことを確認するメッセージが表示されます。

デバイスコンソールユーティリティでドライバーをインストールできなかった場合は、現在の OS プラットフォームとドライバーのプラットフォームに一致するものを使用していることを確認します。

## <a name="view-the-device-in-device-manager"></a>デバイスマネージャーでデバイスを表示する

1. デバイス マネージャーを開きます。 これはさまざまな方法で行うことができますが、コマンドプロンプトがまだ表示されている場合は、「」と入力し `devmgmt` ます。

1. デバイスマネージャーで、[**表示**] メニューの [**種類別のデバイス**] を選択します。

1. デバイスが [ **Samples** ] ノードの下に一覧表示されます。

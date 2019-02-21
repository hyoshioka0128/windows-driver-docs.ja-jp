---
title: 磁気ストライプ リーダーのドライバーのサンプル
description: このサンプルでは、磁気ストライプ リーダーのユニバーサル ドライバーを作成する方法について説明し、新しいドライバーを作成するためのテンプレートとしてためのものです。
ms.assetid: 92A8C116-F71F-4A74-A453-44C14297BCDD
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 529796f950e95f8f19ba8d11af8abd527f1e5c4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529436"
---
# <a name="magnetic-stripe-reader-driver-sample"></a>磁気ストライプ リーダーのドライバーのサンプル

磁気ストライプ リーダーのドライバーのサンプルでは、磁気ストライプ リーダーのユニバーサル ドライバーを作成する方法について説明し、新しいドライバーを作成するためのテンプレートとして使用するためのものがします。 このサンプルでは、ユーザー モード ドライバー フレームワーク (UMDF) 2.0 を使用しと主張して排他アクセスのデバイスなどの基本的な機能を示します。 ドライバーのサンプルをコンパイルし、x86、amd64、上に展開および ARM プラットフォームです。

## <a name="requirements"></a>要件

-   Windows 10
-   [Microsoft Visual Studio 2015](https://go.microsoft.com/fwlink/p/?LinkId=533470) (全バージョン)
-   [Windows Driver Kit (WDK) 10](https://go.microsoft.com/fwlink/p/?LinkId=733614)

Windows ソフトウェア開発キット (SDK) 10 も必要ですが、これは、Microsoft Visual Studio 2015 の一部としてインストールします。

> [!NOTE]
> ドライバーのサンプルでは、磁気ストライプ リーダー ソフトウェア デバイスで動作するために機能するハードウェアは必要ありません。 サンプルで使用するハードウェア デバイスを使っている場合でも、INF ファイルに、デバイスのハードウェア ID を追加してドライバーを使用することができます。

## <a name="download-and-extract-the-sample"></a>ダウンロードして、サンプルの抽出

Windows 10 以降、Windows ドライバーのサンプルは GitHub で入手できからダウンロードできます、 [Windows ドライバーのサンプル リポジトリのプロジェクト ページ](https://go.microsoft.com/fwlink/p/?LinkId=616507)します。

1.  ダウンロード**Windows ドライバーのサンプル-master.zip**から[GitHub](https://go.microsoft.com/fwlink/p/?LinkID=623296)します。 このファイルには、すべての Windows ドライバーのサンプルが含まれています。
2.  抽出**Windows ドライバーのサンプル-master.zip**開発用コンピューターに任意の場所にします。 この場所として参照される*&lt;サンプル\_ルート&gt;* この記事の残りの部分。

## <a name="open-the-driver-solution-in-visual-studio"></a>Visual Studio でのドライバー ソリューションを開く

1.  Windows エクスプ ローラーに移動、`<sample_root>\pos\drivers\MagneticStripeReader\`フォルダー。
2.  ソリューション ファイルをダブルクリックして**MagneticStripeReader.sln**を Visual Studio 2015 でソリューションを開きます。
3.  プロジェクトの zip ファイルは、ソリューションを開いたときにセキュリティの警告を参照してください、インターネットからダウンロードされました。 クリックすると**OK**プロジェクトの読み込みが完了します。
4.  Visual Studio で、検索**ソリューション エクスプ ローラー**します。 これがまだ開いていない場合は、選択**ソリューション エクスプ ローラー**から、**ビュー**メニュー。 **ソリューション エクスプ ローラー**プロジェクトを確認し、ソース ファイルが含まれています。

## <a name="build-the-sample-using-visual-studio"></a>Visual Studio を使用してサンプルをビルドします。

1.  *標準*選択 Visual Studio でのツールバー、*ソリューション プラットフォーム*オペレーティング システムのプラットフォームに一致します。 たとえば、Windows の 64 ビット バージョンを使用している場合は、x64 を選択します。
    > [!NOTE]
    > ARM プラットフォームを対象とする場合は、configuration manager を使用して ARM をターゲットの一覧に追加する必要があります。

2.  選択**ソリューションのビルド**から、**ビルド**メニュー。

## <a name="install-the-driver"></a>ドライバーのインストール

1.  ビルド時に、ドライバーは、テスト証明書で署名されました。 テスト用のドライバーをインストールするには、ブート構成を読み込む、ドライバーがテスト証明書で署名の許可を変更する必要があります。 設定を変更するには、特権のコマンド プロンプトを開くし、コマンドを入力します。

    `bcdedit.exe /set TESTSIGNING on`

2.  コンピューターを再起動します。
    > [!NOTE]
    > テスト署名が有効になっていた場合、再起動は必要はありません。

     

3.  管理者特権のコマンド プロンプトで、プロジェクトがビルドされたフォルダーに移動します。 X64 を作成する場合はデバッグ ビルドでは、このフォルダーに`<project_root>\x64\Debug\SampleMagneticStripeReaderDrv`します。

    そのフォルダーでは、次のファイルが表示されます。

    | ファイル                              | 説明                                                                  |
    |-----------------------------------|------------------------------------------------------------------------------|
    | SampleMagneticStripeReaderDrv.dll | ドライバー ファイルです。                                                             |
    | SampleMagneticStripeReaderDrv.inf | ドライバーをインストールするために必要な情報を格納する INF ファイルを指定します。          |
    | samplemagneticstripereaderdrv.cat | 署名済みカタログ ファイル全体のパッケージの署名として機能します。 |

     

4.  OS およびドライバーのプラットフォームに一致するデバイス コンソール ユーティリティ (devcon.exe) へのパスを特定します。 既定の場所のバージョンが x64`C:\Program Files (x86)\Windows Kits\10\Tools\x64`します。
5.  次に入力してコマンドを置き換える&lt;devcon\_パス&gt;前の手順である devcon.exe ファイルへのパス。

    `"<devcon_path>\devcon.exe" install SampleMagneticStripeReaderDrv.inf Root\SampleMagneticStripeReaderDrv`

6.  表示されます、 **Windows セキュリティ**ドライバーの発行者を検証できないことを通知するダイアログ。 これは、ドライバーは、テスト証明書で署名されたためにです。 クリックして**とにかくこのドライバー ソフトウェアをインストール**します。 この後すぐに、ドライバーが正しくインストールされていることの確認が表示されます。

ドライバーをインストールするデバイス コンソール ユーティリティができなかった場合は、使用している、現在の OS プラットフォームおよびドライバーのプラットフォームと一致することを確認します。

## <a name="view-the-device-in-device-manager"></a>デバイス マネージャーで、デバイスを表示します。

1.  デバイス マネージャーを開きます。 これ行う多くの点が、コマンド プロンプトを入力し、引き続き場合`devmgmt`します。
2.  デバイス マネージャーで、**デバイスの種類によって**から、**ビュー**メニュー。
3.  デバイスは、下に表示されます、**サンプル**ノード。

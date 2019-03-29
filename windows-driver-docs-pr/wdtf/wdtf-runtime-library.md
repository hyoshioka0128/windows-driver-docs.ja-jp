---
title: WDTF ランタイム ライブラリ
description: WDTF ランタイム ライブラリやそれに含まれるツールをインストールする方法の説明です。
keywords:
- WDTF
- Windows ドライバー テスト フレームワーク
- WDTF ランタイム
- WDTF をインストールします。
- ドライバーのテスト
ms.date: 08/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: e0d3456068a930d2ab8f3859709d1e45e0884c86
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136115"
---
# <a name="the-wdtf-runtime-library"></a>WDTF ランタイム ライブラリ

WDTF ランタイム ライブラリが使用可能な Windows Driver Kit (WDK) の一部として。 WDK をインストールするときに、Windows ドライバー テスト フレームワーク (WDTF) をインストールします。 テンプレート ファイルとテストと開発のサンプル ファイルは、WDK と一緒にインストールされます。 WDTF ランタイム ライブラリは、WDTF ベースのテストを実行する任意のシステムにインストールする必要があります。 WDK で提供されるテストが含まれ、WDK を使用して作成するテストは、テンプレートをテストします。

WDK には、テスト コンピューターに WDTF ランタイムをインストールに使用できる個別のインストール パッケージ (*.msi) も含まれています。 MSI は、次を行います。

- ファイルをコピーします。

- レジストリ キーを追加します。

- WDTF オブジェクトを登録します。

- インストールして、ログ ファイルをアンインストールします。

WDTF ランタイム ライブラリには、トリアージ、およびテストの実行に役立つツールが含まれています。

|ツールまたはコマンドのスクリプトの名前|説明|
|----|----|
|CheckWDTFInstall.cmd|WDTF が正しくインストールされていることを確認します。 このコマンドを実行すると、ファイルをすべてインストールされている WDTF コンポーネントに関する情報を含む、CheckWDTFInstall.log が作成されます。|
|DisplayDeviceClass.vbs|現在のシステム上に存在するデバイス クラスの情報を表示します。 クラスの GUID とクラスのフレンドリ名の両方が表示されます。 デバイスの特定のクラスを検索するクエリを/DQ を作成する場合に役立ちます。|
|DisplayDeviceDataFields.cmd|現在のシステム上に存在するデバイス クラスの情報を表示します。 クラスの GUID とクラスのフレンドリ名の両方が表示されます。 デバイスの特定のクラスを検索するクエリを/DQ を作成する場合に役立ちます。|
|DisplayDevices.vbs|/DQ パラメーター、既定値で表される各デバイスに関する情報を表示しますが、システムのすべてのデバイス。 |
|DisplayDevicesWithWDTFilters.vbs|WDTF フィルター ドライバーがインストールされていることのいずれかを含む任意のデバイスが表示されます。 WDTF では、次の 3 つのフィルター ドライバーがあります。EDT、IOSPY、またはボタン ドライバー。|
|DisplayDeviceTree.vbs|デバイスの現在のシステムのツリーが表示されます。|
|DisplaySystemDataFields.cmd|すべてのシステム名前空間や、フィールドが表示されます。|

## <a name="how-to-install-the-wdtf-runtime-library"></a>WDTF ランタイム ライブラリをインストールする方法

展開のテスト コンピューターを設定するとき、WDTF ランタイム ライブラリは、テスト コンピューターにインストールされます。 指示に従って[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 10 および WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)

<!-- [Provision a computer for driver deployment and testing (WDK 8)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8) -->

また、WDTF ランタイム ライブラリを手動でインストールできます。

### <a name="installing-wdtf-on-a-test-computer-preferred-method"></a>テスト コンピューター (優先手段) WDTF をインストールします。

1. Visual Studio をインストールし、WDK をインストールします。

2. テスト用のリモート コンピューターを構成します。 Visual Studio で、をクリックして、**ドライバー**メニューで、**テスト**、 をクリックし、**コンピューターを構成**します。

### <a name="manually-installing-wdtf-on-a-test-computer-alternative-method"></a>テスト コンピューター (代替方法) WDTF を手動でインストールします。

1. Visual Studio と WDK を開発用のコンピューターにインストールします。

2. テスト コンピューターに、WDK をインストールしたコンピューターから WDTF インストール ファイルをコピーします。 WDTF インストール ファイル (*.msi および *.cab ファイル) は、開発システムに %programfiles%\Windows Kits\10\Testing\Runtimes ディレクトリに配置されます。 テスト コンピューターのアーキテクチャに一致するディレクトリ内のすべてのファイルをコピーします。

3. テスト コンピューターで、管理者特権でのアクセス許可を使用してコマンド プロンプト ウィンドウを開きます (**管理者として実行**) WDTF のインストール ファイルを含むディレクトリに移動します。 WDTF をインストールするには、次のコマンドのいずれかを実行します。

    ```cmd
    msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64_en-us.msi"
    ```

    - または -

    ```cmd
    msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x86_en-us.msi"
    ```

次の表は、オプションで使用できる、 **msiexec**コマンド。

|オプション|説明|
|----|----|
|**/l*** *filename*|すべてのメッセージとエラーをファイルに書き込みます*filename*します。|
|**WDTFDIR =**_CustomInstallationDirectory_|WDTF ランタイムのインストール先ディレクトリを指定します。 既定の**WDTFDir** %programfiles%\Windows Kits\10\Testing\Runtimes\WDTF には|
|**WDTF_SKIP_MACHINE_CONFIG = [1 \| 2]。**|指定**1**を既定のスクリプト エンジンとして設定 cscript.exe をスキップします。 指定**2**を有効にすると、ac 電源と DC RTC ウェイク アップをスキップします。|
|**/?**|Msiexec.exe オプションのヘルプを表示します。|

### <a name="example"></a>例

```cmd
msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64_en-us.msi" /l* WDTFInstall.log WDTFDir=c:\wdtf WDTF_SKIP_MACHINE_CONFIG=1
```

## <a name="how-to-determine-if-the-wdtf-runtime-library-is-installed-on-a-compute"></a>コンピューティング、WDTF ランタイム ライブラリがインストールされているかどうかを判断する方法

コマンド スクリプトをテスト コンピューターで実行されている WDTF が正しくインストールされていることを確認できます。 このコマンドを実行すると、ファイルをすべてインストールされている WDTF コンポーネントに関する情報を含む、CheckWDTFInstall.log が作成されます。

1. テスト コンピューターでコマンド プロンプト ウィンドウを開きます。

2. `%WDTFDir%\Tools\CheckWDTFInstall.cmd` を実行します。

3. CheckWDTFInstall.log ログ ファイルを開き、結果を確認します。

## <a name="how-to-uninstall-the-wdtf-runtime-library"></a>WDTF ランタイム ライブラリをアンインストールする方法

設定すると展開については、テスト コンピューターを次の手順については、[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)、WDTF ランタイム ライブラリがターゲット コンピューターにインストールされています。

WDTF ランタイム ライブラリを削除しますするには、対象のコンピュータからプロビジョニングの削除します。 詳細については、次を参照してください。[削除対象のコンピュータからプロビジョニング](https://docs.microsoft.com/windows-hardware/drivers/develop/what-happens-when-you-provision-a-computer--wdk-8-1-#span-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanremoving-provisioning-from-the-target-computer)します。

WDTF ランタイム ライブラリを手動でアンインストールできます。

## <a name="manually-uninstalling-wdtf-on-a-test-computer"></a>テスト コンピューターで WDTF を手動でアンインストールします。

1. テスト コンピューター上に移動**設定**し**アプリ**します。

2. **プログラムと機能**を Windows ドライバー テスト フレームワーク (WDTF) のランタイム ライブラリの検索、右クリックして選択**アンインストール**します。

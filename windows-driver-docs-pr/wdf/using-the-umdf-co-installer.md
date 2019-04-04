---
title: UMDF 共同インストーラーの使用
description: UMDF 共同インストーラーの使用
ms.assetid: e5ec2122-1602-487b-baad-4a3d9e47cf58
keywords:
- UMDF coinstallers WDK
- WDK UMDF 共同インストーラー
- 共同インストーラーが WDK UMDF をセクションします。
- 構成可能な coinstallers WDK UMDF
- システム提供の UMDF 共同インストーラー WDK UMDF
- 再頒布可能パッケージ coinstallers WDK UMDF
- WDK UMDF 共同インストーラーを更新します。
- INF ファイル WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 264d49d80852a5635ed6fd8bac37e55034f28e32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578595"
---
# <a name="using-the-umdf-co-installer"></a>UMDF 共同インストーラーの使用


共同インストーラーは、コンピューターに格納されているフレームワークのバージョンを更新し、フレームワーク固有の INF ファイルのセクションを処理します。 このトピックでは、2 つの UMDF 共同インストーラーとのいずれかに含める必要がある場合について説明します。、[ドライバー インストール パッケージ](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)または INF ファイルで共同インストーラーを参照します。

## <a name="getting-the-co-installer-package"></a>共同インストーラー パッケージを取得します。


Windows 8.1 で再頒布可能フレームワークの Microsoft 提供の更新プログラムが含まれます一部として Windows Driver Kit (WDK) の。

共同インストーラー ディレクトリの内容の完全な一覧を参照してください。 [KMDF ドライバーのインストール コンポーネント](installation-components-for-kmdf-drivers.md)します。

共同インストーラー ディレクトリに含まれるその他のコンポーネント間で、*共同インストーラーを更新*、WUDFUpdate と呼ばれる\_*MMmmm*.dll、場所*MM*メジャーにはバージョン番号、および*mmm*マイナー バージョン番号です。

更新プログラムの共同インストーラーは、コンピューター上にある UMDF フレームワークのバージョンを更新します。 たとえば場合は、コンピューターに UMDF バージョン 1.9 共同インストーラーがバージョン 1.11 を含む、共同インストーラーは、1.11 にコンピューターのフレームワークのバージョンを更新します。

オペレーティング システムにはと呼ばれる別の共同インストーラーが含まれています、*構成共同インストーラー*、または WudfCoinstaller.dll します。 構成の共同インストーラーは、UMDF に固有のセクションでは、ドライバーの INF ファイルを処理し、により、レジストリが、必要な更新します。

## <a name="referencing-co-installers-from-your-inf-file"></a>INF ファイルから co-installer を参照します。


Windows 8.1 用 2.0 の UMDF ドライバーを作成する場合、INF ファイルは、構成共同インストーラーを参照する必要があります。 オペレーティング システムの構成の共同インストーラーが含まれている、ために、再配布する必要はありません。

作成する場合、ドライバーを使用するマシンを Windows 8.1 以前のオペレーティング システムをターゲット、ことをフレームワークのバージョン 1.11 UMDF 1.11 ドライバーがインストールされています。 これを行う 3 つの方法を次に示します。

-   INF ファイルで更新プログラムの共同インストーラーを参照してで更新プログラムの共同インストーラーを含める、[ドライバー インストール パッケージ](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)します。 オペレーティング システムが、ドライバーをインストールするときは、共同インストーラーを実行します。 ドライバーは、Windows Update を使用して分散は、このオプションを選択する必要があります。

-   関連する MSU パッケージ (たとえば umdf-1.11-Win-6.0.msu) を呼び出すセットアップ アプリケーションと共に再配布します。 Src でこのようなアプリケーションのサンプルが見つかります\\全般\\WDK インストールの wdkinstall サブディレクトリ。 デバイスに付属し、デバイスを使用する前に実行する必要があるセットアップ プログラムを記述する場合は、このオプションを選択する可能性があります。 このオプションを選択した場合、INF ファイルは、構成共同インストーラーを参照する必要があります。

-   ドライバーを使用するマシンに必要なフレームワーク バージョンをインストールする Windows 更新プログラムに依存します。 UMDF の新しいバージョンは、framework のバージョン 1.11 以降、Windows Update 経由で配布されます。 このオプションを選択した場合、INF ファイルは、構成共同インストーラーを参照する必要があります。

INF ファイルで更新プログラムの共同インストーラーまたは構成の共同インストーラーを常に参照する必要があります。 ただし、両方の共同インストーラー、INF で参照するエラーにつながるインストール。

## <a name="inf-file-sections-for-the-co-installer"></a>共同インストーラーのセクションでは INF ファイル


ドライバーの INF ファイルを含める必要があります、 [ **INF DDInstall.CoInstallers セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547321)します。 更新プログラムの共同インストーラーを再配布する場合、 **DDInstall.CoInstallers**セクションは、両方を含める必要があります、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)と[ **INF CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)、次の例を示しています。

```cpp
[MyDriver_Install.CoInstallers]
AddReg = MyDriver_Install.CoInstallers_AddReg
CopyFiles = MyDriver_CoInstallers_CopyFiles
```

INF **AddReg**ディレクティブを作成する INF セクションを識別、 **CoInstallers32**レジストリ エントリ。

```cpp
[MyDriver_Install.CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,"WudfUpdate_01011.dll"
```

INF **CopyFiles**ディレクティブは、システムのデバイスにインストール デバイスから共同インストーラーをコピーする INF セクションを識別します。

```cpp
[MyDriver_CoInstallers_CopyFiles]
WudfUpdate_01011.dll
```

MSU パッケージでは、再配布する場合、 **DDInstall.CoInstallers**セクションを指定する必要があります、 **AddReg**構成共同インストーラーを参照するディレクティブ。

```cpp
[Echo_Install.NT.CoInstallers]
AddReg=CoInstallers_AddReg
[CoInstaller.AddReg]
HKR,,CoInstallers32,0x00010000,WudfCoinstaller.dll
```

ドライバーの INF ファイルは常に含める必要があります、 **DDInstall.Wdf**共同インストーラーがインストールされていた後を読み取っていることをセクションします。 ドライバーを指定できますディレクティブについては**DDInstall.Wdf**を参照してください[INF ファイルで WDF ディレクティブを指定する](specifying-wdf-directives-in-inf-files.md)します。

INX ファイルを使用して複数のバージョンの framework の複数の INF ファイルを作成しなくて済みます、 [Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)ツール。 INX ファイルの詳細については、[INX INF ファイルを作成するファイルを使用する](using-inx-files-to-create-inf-files.md)を参照してください。

 

 






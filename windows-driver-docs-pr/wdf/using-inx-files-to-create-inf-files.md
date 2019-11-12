---
title: INX ファイルを使用した INF ファイルの作成
description: INX ファイルを使用した INF ファイルの作成
ms.assetid: b49f8fed-c2b5-46e2-aeaf-e09231fa1578
keywords:
- INX ファイル WDK KMDF
- ビルドユーティリティ WDK KMDF
- Stampinf WDK KMDF
- KMDF WDK、INX ファイル
- カーネルモードドライバーフレームワーク WDK、INX ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 367768bcd95cd413b72a674a8fb04cd43f6354f1
ms.sourcegitcommit: 134bbe010add8cf161a82d9cccac084bb6931d32
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2019
ms.locfileid: "73914928"
---
# <a name="using-inx-files-to-create-inf-files"></a>INX ファイルを使用した INF ファイルの作成


*INX ファイル*は、バージョン情報を表す文字列変数を含む INF ファイルです。 Microsoft Visual Studio を使用してドライバーをビルドすると、ビルドプロセスによって[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)ツールが実行され、INX ファイル内の文字列変数が、特定のハードウェアアーキテクチャまたはフレームワークバージョンを表すテキスト文字列に置き換えられます。 また、Stampinf ツールを手動で実行することもできます。このツールは、WDK の*bin*サブディレクトリにあります。

ドライバーの INX ファイルを作成する場合、複数のバージョン固有の INF ファイルを保持する必要はありません。 代わりに、1つの INX ファイルを作成し、Visual Studio または Stampinf を使用して、必要に応じてバージョン固有の INF ファイルを生成することができます。

Visual Studio 内の Stampinf プロパティを変更するには、ドライバーパッケージプロジェクトのプロパティページを開きます。 ソリューションエクスプローラーでパッケージプロジェクトを右クリックし、 **[プロパティ]** を選択します。 パッケージのプロパティページで、 **[構成プロパティ]** をクリックし、 **[StampInf]** をクリックします。

WDK には、すべての KMDF および UMDF サンプルドライバー用の INX ファイルが含まれています。

INX ファイルには、次の文字列変数を含めることができます。

<a href="" id="-arch-"></a>$ARCH $  
Stampinf は、この変数をアーキテクチャ固有の文字列に置き換えます。 たとえば、x86 ビルド環境を使用している場合は、$ARCH $ が "x86" に置き換えられます。 次のように[ **、inf ファイル**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)内で特定のアーキテクチャを指定するために必要な場所であればどこでも $ARCH $ string を使用できます。

```cpp
[Manufacturer]
%StdMfg%=Standard,NT$ARCH$
```

<a href="" id="-kmdfcoinstallerversion-"></a>$KMDFCOINSTALLERVERSION $  
[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)ツールの-*k*オプションを使用すると、Stampinf は、この変数を kmdf 共同インストーラーの特定のバージョンを表す文字列に置き換えます。 $KMDFCOINSTALLERVERSION $ 変数は、次のように、inf [**Ddinstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section)内で、フレームワークの共同インストーラーを inf ファイル内で指定するときに使用できます。

```cpp
[ECHO_Device.NT.CoInstallers]
AddReg=ECHO_Device_CoInstaller_AddReg
CopyFiles=ECHO_Device_CoInstaller_CopyFiles

[ECHO_Device_CoInstaller_AddReg]
HKR,,CoInstallers32,0x00010000, "WdfCoInstaller$KMDFCOINSTALLERVERSION$.dll,WdfCoInstaller"

[ECHO_Device_CoInstaller_CopyFiles]
WdfCoInstaller$KMDFCOINSTALLERVERSION$.dll
```

<a href="" id="-kmdfversion-"></a>$KMDFVERSION $  
Visual Studio で**Kmdf バージョン番号**プロパティを設定した場合 (または[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)ツールの-*k*オプションを使用した場合)、Stampinf は、この変数を kmdf の特定のバージョンを表す文字列に置き換えます。 $KMDFVERSION $ 変数は、次のように[Kmdflibraryversion](installing-the-framework-s-co-installer.md)ディレクティブを指定する場合など、INF ファイル内でフレームワークのバージョンを指定するときに使用できます。

```cpp
KmdfLibraryVersion = $KMDFVERSION$
```

<a href="" id="-umdfcoinstallerversion-"></a>$UMDFCOINSTALLERVERSION $  
```cpp
[SourceDisksFiles]
WudfUpdate_$UMDFCOINSTALLERVERSION$.dll=1

[CoInstallers_CopyFiles]
WudfUpdate_$UMDFCOINSTALLERVERSION$.dll

[CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,"WUDFUpdate_$UMDFCOINSTALLERVERSION$.dll"
```

<a href="" id="-umdfversion-"></a>$UMDFVERSION $  
```cpp
[UMDFYourDriver_Install]
UmdfLibraryVersion=$UMDFVERSION$
```

[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)では、INX ファイル内の UMDF 文字列変数を置き換える-*u*オプションもサポートされています。 ドライバーパッケージに、UMDF ベースのドライバーと KMDF ベースのドライバーの両方が含まれている場合は、1つの Stampinf コマンドと1つの INX ファイルで-*k*および-*u*オプションを使用できます。

 

 






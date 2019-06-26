---
title: INX ファイルを使用した INF ファイルの作成
description: INX ファイルを使用した INF ファイルの作成
ms.assetid: b49f8fed-c2b5-46e2-aeaf-e09231fa1578
keywords:
- INX は、WDK KMDF をファイルします。
- WDK KMDF ユーティリティを構築します。
- Stampinf WDK KMDF
- KMDF WDK、INX ファイル
- カーネル モード ドライバー フレームワーク WDK、INX ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cec8dd4eee644b0a5057d93f307735d6392e7073
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372245"
---
# <a name="using-inx-files-to-create-inf-files"></a>INX ファイルを使用した INF ファイルの作成


*INX ファイル*INF ファイル バージョン情報を表す文字列変数を含むです。 Microsoft Visual Studio を使用してドライバーをビルドすると、ビルド プロセスの実行、 [Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf) INX で文字列変数を置換するためのツールが特定のハードウェア アーキテクチャまたはフレームワークのバージョンを表すテキスト文字列を持つファイルします。 ある Stampinf ツールも手動で実行することができます、 *bin* WDK のサブディレクトリ。

ドライバーの INX ファイルを作成する場合は、複数のバージョンに固有の INF ファイルを維持する必要はありません。 代わりに、1 つ INX ファイルを作成し、必要なときに、バージョン固有の INF ファイルを生成する Visual Studio または Stampinf を使用することができます。

Visual Studio 内で Stampinf プロパティを変更するには、ドライバー パッケージ プロジェクトのプロパティ ページを開きます。 ソリューション エクスプ ローラーでパッケージ プロジェクトを右クリックして**プロパティ**します。 パッケージのプロパティ ページで次のようにクリックします。**構成プロパティ**、し**StampInf**します。

ある Stampinf ツールも手動で実行することができます、 *bin* WDK のサブディレクトリ。

WDK には、すべて、KMDF ドライバーおよび UMDF サンプル ドライバーの INX ファイルが含まれています。

INX ファイルは、次の文字列変数を含めることができます。

<a href="" id="-arch-"></a>$ARCH$  
Stampinf は、この変数をアーキテクチャ固有の文字列に置き換えます。 たとえば、x86 を使用しているビルド環境、ツールの後継 $ARCH$"x86"にします。 $ARCH$ の文字列を使用するには、内で、INF ファイル内の特定のアーキテクチャを指定する必要がある場合、 [ **INF 製造元セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)、次のように。

```cpp
[Manufacturer]
%StdMfg%=Standard,NT$ARCH$
```

<a href="" id="-kmdfcoinstallerversion-"></a>$KMDFCOINSTALLERVERSION $  
使用する場合、 [Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)ツールの -*k*オプション、Stampinf で、KMDF 共同インストーラーの特定のバージョンを表す文字列でこの変数が置き換えられます。 内など、INF ファイル内のフレームワークの共同インストーラーを指定する場合は、$KMDFCOINSTALLERVERSION の $ 変数を使用することができます、 [ **INF DDInstall.CoInstallers セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section)、次のようにします。

```cpp
[ECHO_Device.NT.CoInstallers]
AddReg=ECHO_Device_CoInstaller_AddReg
CopyFiles=ECHO_Device_CoInstaller_CopyFiles

[ECHO_Device_CoInstaller_AddReg]
HKR,,CoInstallers32,0x00010000, "WdfCoInstaller$KMDFCOINSTALLERVERSION$.dll,WdfCoInstaller"

[ECHO_Device_CoInstaller_CopyFiles]
WdfCoInstaller$KMDFCOINSTALLERVERSION$.dll
```

<a href="" id="-kmdfversion-"></a>$KMDFVERSION$  
設定した場合、 **KMDF バージョン番号**Visual Studio でのプロパティ (を使用して、または、 [Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)ツールの -*k*オプション)、Stampinf を表す文字列でこの変数が置き換えられます、KMDF の特定のバージョン。 $KMDFVERSION$ 変数を使用するには、指定した場合など、INF ファイル内のフレームワークのバージョンを指定すると、 [KmdfLibraryVersion](installing-the-framework-s-co-installer.md)ディレクティブを次のとおりです。

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

<a href="" id="-umdfversion-"></a>$UMDFVERSION$  
```cpp
[UMDFYourDriver_Install]
UmdfLibraryVersion=$UMDFVERSION$
```

[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)もサポートしています-*u* INX ファイル UMDF 文字列変数を置換するオプション。 使用することができます、ドライバー パッケージには、UMDF ベースのドライバーと KMDF ベースのドライバーの両方が含まれている場合-*k*と -*u* Stampinf コマンドを 1 つと、1 つの INX ファイル オプション。

 

 






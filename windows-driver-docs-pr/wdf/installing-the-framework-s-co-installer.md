---
title: INF ファイルでの KMDF 共同インストーラーの指定
description: ドライバーパッケージに共同インストーラーを含める場合は、ドライバーの INF ファイルに入力する必要があるセクションの詳細について、このトピックを参照してください。
ms.assetid: e4f476ad-1ab5-44e3-9368-7467479bda85
keywords:
- カーネルモードドライバーフレームワーク WDK、ドライバーのインストール
- フレームワークベースのドライバー WDK KMDF, インストール
- INF ファイル WDK KMDF、coinstallers
- coinstallers WDK KMDF
- CoInstallers セクション WDK KMDF
- DDInstall セクション WDK KMDF
- Wdf INF ファイルセクション WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4dbc60269f33d37d2e77205220bc57d6f3e63b6
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073425"
---
# <a name="specifying-the-kmdf-co-installer-in-an-inf-file"></a>INF ファイルでの KMDF 共同インストーラーの指定


[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/components-of-a-driver-package)に共同インストーラーを含める場合は、ドライバーの INF ファイルに入力する必要があるセクションの詳細について、このトピックを参照してください。 この情報は、Microsoft が提供する .msu 再頒布可能パッケージを呼び出す独自のセットアップアプリケーションを提供する場合には適用されません。

##  <a name="inf-file-sections-for-the-co-installer"></a>共同インストーラーの INF ファイルのセクション


ドライバーの INF ファイルには、INF <em>Ddinstall</em>が含まれている必要があり**ます。CoInstallers**セクション。共同インストーラーをインストールします。 たとえば、このセクションには ntx86 という名前が付けられます。 **CoInstallers**です。 INF ファイルでの共同インストーラーの指定の詳細については、「 [**Inf Ddinstall」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section)を参照してください。

また、ドライバーの INF ファイルには、INF <em>Ddinstall</em>が含まれている必要があり**ます。Wdf**セクションは、インストール後に共同インストーラーによって読み取られます。 たとえば、このセクションには ntx86 という名前が付けられます。 **Wdf**です。 フレームワークの共同インストーラーがインストールされると、ドライバーのインストール中にこのセクションが読み取られます。

INF <em>Ddinstall</em>**。Wdf** section には、次のディレクティブが含まれています。

- **Kmdfservice =** <em>driverservice</em>**、**<em>Wdf</em>

*Driverservice*は、オペレーティングシステムによってドライバーのカーネルモードサービスに割り当てられる名前を表し、 *Wdf*は、ドライバーに関する情報を取得するために、共同インストーラーが読み取る INF セクションの名前を表します。

*Wdf*によって識別される INF セクションには、次のディレクティブが含まれている必要があります。

-   **Kmdflibraryversion =** *wdflibraryversion*

*Wdflibraryversion*は、"1.0" や "1.11" などのライブラリのバージョン番号を表します。

たとえば、次の INF <em>Ddinstall がインストール</em>されていると**します。Wdf**セクションでは、 *Wdf*という名前の**Echo \_ wdfsect**を指定します。

```cpp
[ECHO_Device.NT.Wdf]
KmdfService = Echo, Echo_wdfsect
[Echo_wdfsect]
KmdfLibraryVersion = 1.0
```

INX ファイルと[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)ツールを使用すると、複数のバージョンのフレームワークに対して複数の INF ファイルを作成することを回避できます。 INX ファイルの詳細については、「 [USING INX files To CREATE INF files](using-inx-files-to-create-inf-files.md)」を参照してください。

### <a name="sample-inf-ddinstallcoinstallers-and-ddinstallwdf-sections"></a><a href="" id="sample-inf-ddinstall-coinstallers-and-ddinstall-wdf-sections"></a>**サンプル INF** ***Ddinstall *。CoInstallers および** * **ddinstall *.Wdf セクション**

次のコード例は、INF <em>Ddinstall</em>を作成する方法を示して**います。CoInstallers** section および INF <em>ddinstall</em>**。** PnP ドライバー用の INF ファイルの Wdf セクション。 この例では、 *Mydevice .inf*という名前の inf ファイルを作成する方法を示します。このファイルは、 [echo](https://go.microsoft.com/fwlink/p/?linkid=256129)サンプルドライバーの*echo .inf*ファイルに基づいています。 Echo サンプルドライバーは、WDK の samples ディレクトリにあります。

*Mydevice .inf*を作成するには、 *modem.inf*のすべての**echo \_ デバイス**の部分文字列を、製品に適した名前に変更する必要があります。 次のコード例では、 **Mydevice**を使用します。

*Echo*サンプルで使用するセクションレイアウトとの一致を試みる必要があります。 言い換えると、可能であれば、共同インストーラーに関連するセクションをまとめて、切り取りと貼り付けのエラーをより簡単に見つけられるようにしてください。

*Echo .inf*を変更する前に、共同インストーラーをインストールするセクションは次のようになります。

```cpp
=============== Top of Echo.inf ====================
....
....
[DestinationDirs]
DefaultDestDir = 12
ECHO_Device_CoInstaller_CopyFiles = 11
....
....
;
;--- ECHO_Device Co-installer installation ------
;
[ECHO_Device.NT.CoInstallers]
AddReg=ECHO_Device_CoInstaller_AddReg
CopyFiles=ECHO_Device_CoInstaller_CopyFiles

[ECHO_Device_CoInstaller_AddReg]
HKR,,CoInstallers32,0x00010000, "WdfCoInstaller01000.dll,WdfCoInstaller"

[ECHO_Device_CoInstaller_CopyFiles]
WdfCoInstaller01000.dll

[ECHO_Device.NT.Wdf]
KmdfService = Echo, Echo_wdfsect
[Echo_wdfsect]
KmdfLibraryVersion = 1.0

===============  End of Echo.inf ===============
```

すべての**ECHO \_ デバイス**の部分文字列を変更した後、 *mydevice .inf*ファイルは次のように表示されます。

```cpp
=============== Top of MyDevice.inf ===============
....
....
[DestinationDirs]
DefaultDestDir = 12
MyDevice_CoInstaller_CopyFiles = 11
....
....
;
;--- MyDevice Co-installer installation ------
;
[MyDevice.NT.CoInstallers]
AddReg=MyDevice_CoInstaller_AddReg
CopyFiles=MyDevice_CoInstaller_CopyFiles

[MyDevice_CoInstaller_AddReg]
HKR,,CoInstallers32,0x00010000, "WdfCoInstaller01000.dll,WdfCoInstaller"

[MyDevice_CoInstaller_CopyFiles]
WdfCoInstaller01000.dll

[MyDevice.NT.Wdf]
KmdfService = MyDevice, MyDevice_wdfsect
[MyDevice_wdfsect]
KmdfLibraryVersion = 1.0
....
....
=============== End of MyDevice.inf ===============
```

 

 






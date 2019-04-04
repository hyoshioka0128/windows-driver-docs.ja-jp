---
title: KMDF 共同インストーラーを INF ファイルで指定します。
description: 共同インストーラーをドライバー パッケージに含める場合は、ドライバーの INF ファイルで指定する必要がありますセクションに関する情報は、このトピックを読み取ります。
ms.assetid: e4f476ad-1ab5-44e3-9368-7467479bda85
keywords:
- カーネル モード ドライバー フレームワーク WDK は、ドライバーをインストールします。
- フレームワーク ベースのドライバー WDK KMDF をインストールします。
- INF ファイル WDK KMDF、共同インストーラー
- WDK KMDF 共同インストーラー
- 共同インストーラーが WDK KMDF をセクションします。
- DDInstall セクション WDK KMDF
- Wdf の INF ファイル セクション WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d345625221a546ad4f612e3fb7b3b5fc33c7fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572660"
---
# <a name="specifying-the-kmdf-co-installer-in-an-inf-file"></a>KMDF 共同インストーラーを INF ファイルで指定します。


共同インストーラーを含める場合は、[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff539954)ドライバーの INF ファイルで指定する必要がありますセクションに関する情報は、このトピックの読み取り。 この情報は、Microsoft 提供の .msu 再頒布可能パッケージを呼び出す独自のセットアップ アプリケーションを提供する場合に適用されません。

##  <a name="inf-file-sections-for-the-co-installer"></a>共同インストーラーのセクションでは INF ファイル


ドライバーの INF ファイルは、INF を含める必要があります<em>DDInstall</em>**します。CoInstallers**共同インストーラーがインストール セクション。 このセクションの名前など**MyDevice.ntx86.CoInstallers**します。 INF ファイルで共同インストーラーを指定する方法については、[ **INF DDInstall.CoInstallers セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547321)を参照してください。

さらに、ドライバーの INF ファイルは、INF を含める必要があります<em>DDInstall</em>**します。Wdf**共同インストーラーがインストールされていた後を読み取っていることをセクションします。 このセクションの名前など、 **MyDevice.ntx86.Wdf**します。 フレームワークの共同インストーラーがインストールされた後は、ドライバーをインストールしているときに、このセクションを読み取ります。

INF <em>DDInstall</em>**します。Wdf**セクションには、次のディレクティブが含まれています。

- **KmdfService =** <em>DriverService</em>**、**<em>Wdf のインストール-セクション</em>

*DriverService*オペレーティング システムが、ドライバーのカーネル モードのサービスに割り当てる名前を表すと*Wdf のインストール-セクション*共同インストーラーを取得する読み取りする INF セクションの名前を表しますドライバーに関する情報。

INF セクション*Wdf のインストール-セクション*識別する必要があります、次のディレクティブを含めます。

-   **KmdfLibraryVersion =** *WdfLibraryVersion*

*WdfLibraryVersion* 「1.0」や「1.11」など、ライブラリのバージョン番号を表します。

次の INF など<em>DDInstall</em>**します。Wdf**セクションを指定します**エコー\_wdfsect**として、 *Wdf のインストール-セクション*名。

```cpp
[ECHO_Device.NT.Wdf]
KmdfService = Echo, Echo_wdfsect
[Echo_wdfsect]
KmdfLibraryVersion = 1.0
```

INX ファイルを使用して複数のバージョンの framework の複数の INF ファイルを作成しなくて済みます、 [Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)ツール。 INX ファイルの詳細については、[INX INF ファイルを作成するファイルを使用する](using-inx-files-to-create-inf-files.md)を参照してください。

### <a href="" id="sample-inf-ddinstall-coinstallers-and-ddinstall-wdf-sections"></a>**サンプル INF** * **DDInstall *。共同インストーラーと** * **DDInstall *。Wdf のセクションでは**

次のコード例は、INF を作成する方法を示します<em>DDInstall</em>**します。CoInstallers**セクションと INF <em>DDInstall</em>**します。Wdf** PnP ドライバーの INF ファイルのセクション。 例では、呼び出される INF ファイルを作成する方法を示しています。 *MyDevice.inf*に基づく、[エコー](https://go.microsoft.com/fwlink/p/?linkid=256129)サンプル ドライバーの*Echo.inf*ファイル。 Echo サンプル ドライバーは、WDK の samples ディレクトリにあります。

作成する*MyDevice.inf*、すべてを変更する必要があります**エコー\_デバイス**で部分文字列を*Echo.inf*製品の適切な名前にします。 次のコード例では**MyDevice**します。

セクションのレイアウトと一致しようとする必要がありますが、 *Echo.inf*サンプルの使用。 つまり、可能であれば、まとめておくため共同 installer に関連するセクションでは、切り取りと貼り付けのエラーをより簡単に特定します。

前に、変更した*echo.inf*、共同インストーラーをインストールするためのセクションでは、次のとおり。

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

すべてを変更した後**エコー\_デバイス**の部分文字列、 *MyDevice.inf*ファイルが次のように表示されます。

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

[MyDevice_Device.NT.Wdf]
KmdfService = MyDevice, MyDevice_wdfsect
[MyDevice_wdfsect]
KmdfLibraryVersion = 1.0
....
....
=============== End of MyDevice.inf ===============
```

 

 






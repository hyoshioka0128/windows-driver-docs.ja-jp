---
title: シェルと自動再生のベンダーのアイコンを提供します。
description: シェルと自動再生のベンダーのアイコンを提供します。
ms.assetid: 2e3afbf6-57f6-4b83-b10a-c33d9b1c1731
keywords:
- 自動再生アイコン WDK
- カスタム アイコン WDK デバイスのインストール
- WDK の仕入先アイコン
- WDK のシェルのアイコン
- Shell アイコン WDK
- WDK メディアに挿入されたアイコン
- WDK なしにメディアで挿入されたアイコン
- WDK の自動再生のアイコン
- アイコン ファイルのコピー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a418b127b32be34732dc2882f3fbd39a20984794
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528498"
---
# <a name="providing-vendor-icons-for-the-shell-and-autoplay"></a>シェルと自動再生のベンダーのアイコンを提供します。





[自動再生](https://go.microsoft.com/fwlink/p/?linkid=12031)シェルの拡張機能は、Microsoft Windows XP と Windows の以降のバージョンでサポートされます。 自動再生では、さまざまな種類のリムーバブル メディアまたはリムーバブル デバイスのオーディオまたはビデオ ファイルなどのコンテンツを検出します。 自動再生がコンテンツと、デバイス用のカスタム アイコンを表示し、再生またはメディアまたはデバイスが検出されときにコンテンツを表示するアプリケーションを自動的に開始することができます。

このトピックでは、デバイスのカスタム アイコンを提供する方法について説明します。 シェルと自動再生は、これらのアイコンを使用して、自動再生、マイ コンピューター、およびファイルの [開く] ダイアログ ボックスでデバイスを表します。 アイコンは、デバイスが存在するかどうかと、メディアが挿入されるかどうかを示します。 次のアイコンを行うことができます。

-   *アイコンのメディアに挿入された*デバイスが存在して、メディアが挿入されることを示します。

-   *アイコンのないメディア挿入*デバイスが存在するが、メディアが挿入されていないことを示します。

個々 のデバイスのアイコンを指定するだけでなく指定することもすべてのデバイスのアイコンをユーザー定義のデバイス グループまたは[デバイス セットアップ クラス](device-setup-classes.md)します。 詳細については、次を参照してください。、[ハードウェアの準備と自動再生で使用するためのソフトウェア](https://go.microsoft.com/fwlink/p/?linkid=12032)web サイト。

場合、更新された[ドライバー パッケージ](driver-packages.md)カスタムを格納しているにアイコンが投稿された[Windows Update](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)ユーザーは新しいダウンロードが利用できるように求められます。

アイコン ファイルを含むドライバー パッケージ内に 2 つの手順があります。

1.  ドライバー パッケージには、アイコン ファイルを追加します。

2.  パッケージの INF ファイルでは、アイコン ファイルを指定し、システムにコピーされるエントリを追加します。

システム指定のドライバーでは、デバイスを処理する場合は完全なを指定する必要はありません[ドライバー パッケージ](driver-packages.md)します。 INF ファイルとアイコン ファイルを提供するだけ済みます。 この INF ファイルは、必要なアイコンに固有のエントリを含める必要があります plus **Include**と**必要がある**エントリをシステム提供のドライバーの INF ファイルで、デバイスのインストールの説明を参照してください。

### <a name="to-create-icons"></a>アイコンを作成するには

-   作成に用意されているガイドラインに従う[Windows XP のアイコン](https://go.microsoft.com/fwlink/p/?linkid=6938)web サイト。 次のガイドラインでは、Windows XP のグラフィカル要素の動作と外観を持つアイコンを作成する方法について説明します。

### <a name="to-specify-the-icons-in-an-inf-file"></a>INF ファイルのアイコンを指定するには

-   含まれて、 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)下、 [ **INF DDInstall.HW セクション**](inf-ddinstall-hw-section.md)デバイス。 **AddReg**セクションで、指定**アイコン**と**NoMediaIcons**の次の例に示すように、エントリの値します。

    ```cpp
    [DDInstall.NT.HW]
    AddReg = IconInformation

    [IconInformation]
    HKR, , Icons, 0x10000, "media-inserted-icon-file"
    HKR, , NoMediaIcons, 0x10000, "no-media-inserted-icon-file"
    ```

    <a href="" id="icons"></a>**アイコン**  
    メディアに挿入されたアイコンを含むファイルの名前を指定します。 *メディアの挿入-アイコン-ファイル*値は実際のファイル名のプレース ホルダーです。

    <a href="" id="nomediaicons"></a>**NoMediaIcons**  
    いいえ-メディアの挿入 アイコンを含むファイルの名前を指定します。 *いいえ-メディアの挿入-アイコン-ファイル*値は実際のファイル名のプレース ホルダーです。

### <a href="" id="to-direct-setup-to-copy-the-icon-files-to-the-system"></a>直接の Windows システムにアイコン ファイルをコピーするには

-   含める、 [ **INF SourceDisksFiles セクション**](inf-sourcedisksfiles-section.md)アイコン ファイルと対応する一覧を示す[ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)をコピーします。システムにします。

Windows の保存、**アイコン**と**NoMediaIcons**の下のエントリの値、**デバイス パラメーター** デバイスのキー*ハードウェア キー*。 次の例は、レジストリの場所、値、エントリの種類の値を指定します、**アイコン**と**NoMediaIcons**デバイス インスタンス ID は USB デバイスのエントリの値\\Vid_0000 & Pid_0000\\059B003112010E93 します。

**HKEY_LOCAL_MACHINE\\システム\\CurrentControlSet\\Enum\\**<em>USB\\Vid_0000 & Pid_0000\\059B003112010E93</em>\\**デバイス パラメーター**

**Icons** \[REG_MULTI_SZ\] = %*SystemRoo*t%*\\system32\\icon.ico*

**NoMediaIcons** \[REG_MULTI_SZ\] % =*SystemRoot*%*\\system32\\noicon.ico*

ドライバーやその他のコードは決してアクセスまたは変更、**デバイス パラメーター**直接キーします。 代わりに、次のシステム関数を使用する必要があります。

-   ユーザーのモードから[ **SetupDiCreateDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550973)と[ **SetupDiOpenDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552079)します。

-   カーネル モードから使用して[ **IoOpenDeviceRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff549443)します。

 

 






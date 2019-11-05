---
title: シェルと自動再生用のベンダー アイコンの提供
description: シェルと自動再生用のベンダー アイコンの提供
ms.assetid: 2e3afbf6-57f6-4b83-b10a-c33d9b1c1731
keywords:
- 自動再生アイコン WDK
- カスタムアイコン WDK デバイスのインストール
- ベンダアイコン WDK
- アイコン WDK シェル
- シェルアイコン WDK
- メディアに挿入されたアイコン WDK
- メディアが挿入されていないアイコン WDK
- アイコン WDK 自動再生
- アイコンファイルをコピーする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7fd17e7b5b1d062c68ce3e1a1c1be433ba77376
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837377"
---
# <a name="providing-vendor-icons-for-the-shell-and-autoplay"></a>シェルと自動再生用のベンダー アイコンの提供





[自動再生](https://go.microsoft.com/fwlink/p/?linkid=12031)は、シェルの拡張機能であり、MICROSOFT windows XP 以降のバージョンの windows でサポートされています。 自動再生では、リムーバブルメディアまたはリムーバブルデバイスで、オーディオファイルやビデオファイルなどのさまざまな種類のコンテンツが検出されます。 自動再生では、コンテンツとデバイスのカスタムアイコンを表示できます。また、システムが中またはデバイスを検出したときに、アプリケーションを自動的に起動してコンテンツを再生または表示することができます。

このトピックでは、デバイスのカスタムアイコンを提供する方法について説明します。 シェルと自動再生では、これらのアイコンを使用して、[自動再生]、[マイコンピューター]、[ファイルを開く] の各ダイアログボックスでデバイスを表します。 アイコンは、デバイスが存在するかどうか、およびメディアが挿入されているかどうかを示します。 次のアイコンを指定できます。

-   *メディアに挿入*されたアイコンは、デバイスが存在し、メディアが挿入されていることを示します。

-   *メディアが挿入*されていないアイコンは、デバイスが存在するがメディアが挿入されていないことを示します。

個々のデバイスのアイコンを指定するだけでなく、ユーザー定義デバイスグループまたは[デバイスセットアップクラス](device-setup-classes.md)のすべてのデバイスのアイコンを指定することもできます。 詳細については、「[自動再生 web サイトで使用するハードウェアとソフトウェアの準備](https://go.microsoft.com/fwlink/p/?linkid=12032)」を参照してください。

カスタムアイコンが含まれている更新された[ドライバーパッケージ](driver-packages.md)が[Windows Update](https://docs.microsoft.com/windows-hardware/drivers)に投稿されている場合は、新しいダウンロードを利用できることをユーザーに確認するメッセージが表示されます。

ドライバーパッケージにアイコンファイルを含めるには、次の2つの手順を実行します。

1.  アイコンファイルをドライバーパッケージに追加します。

2.  パッケージの INF ファイルで、アイコンファイルを指定するエントリを追加し、システムにコピーします。

システム提供のドライバーがデバイスを処理する場合は、完全な[ドライバーパッケージ](driver-packages.md)を提供する必要はありません。 INF ファイルとアイコンファイルを指定するだけで済みます。 この INF ファイルには、必要なアイコン固有のエントリに加えて **、システム**が提供するドライバーの INF ファイルにあるデバイスのインストールセクションを参照するエントリが**含ま**れている必要があります。

### <a name="to-create-icons"></a>アイコンを作成するには

-   「 [WINDOWS XP アイコン](https://go.microsoft.com/fwlink/p/?linkid=6938)の作成」 web サイトに記載されているガイドラインに従ってください。 これらのガイドラインでは、Windows XP のグラフィカル要素の外観と動作を持つアイコンを作成する方法について説明します。

### <a name="to-specify-the-icons-in-an-inf-file"></a>INF ファイルのアイコンを指定するには

-   Inf [**AddReg ディレクティブ**](inf-addreg-directive.md)をデバイスの[**inf DDINSTALL. HW セクション**](inf-ddinstall-hw-section.md)に含めます。 **[AddReg]** セクションで、次の例に示すように、**アイコン**と**nomediaicons**の値のエントリを指定します。

    ```cpp
    [DDInstall.NT.HW]
    AddReg = IconInformation

    [IconInformation]
    HKR, , Icons, 0x10000, "media-inserted-icon-file"
    HKR, , NoMediaIcons, 0x10000, "no-media-inserted-icon-file"
    ```

    <a href="" id="icons"></a>**アイコン**  
    メディアに挿入されたアイコンを含むファイルの名前を指定します。 *メディアに挿入*されたアイコンファイルの値は、実際のファイル名のプレースホルダーです。

    <a href="" id="nomediaicons"></a>**NoMediaIcons**  
    メディアに挿入されていないアイコンを含むファイルの名前を指定します。 *メディアに挿入*されていないファイルの値は、実際のファイル名のプレースホルダーです。

### <a href="" id="to-direct-setup-to-copy-the-icon-files-to-the-system"></a>アイコンファイルをシステムにコピーするように Windows に指示するには

-   アイコンファイルと、それらをシステムにコピーする対応する[**Inf CopyFiles ディレクティブ**](inf-copyfiles-directive.md)を一覧表示する[**Inf SourceDisksFiles セクション**](inf-sourcedisksfiles-section.md)をインクルードします。

Windows では、デバイスの*ハードウェアキー*の下に、**デバイスパラメーター**キーの下に**アイコン**および**nomediaicons**の値のエントリが保存されます。 次の例では、デバイスインスタンス ID が USB\\Vid_0000 & Pid_0000\\059B003112010E93 であるデバイスについて、レジストリの場所、値のエントリの種類、および**アイコン**と**nomediaicons**の値のエントリを指定します。

**HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\** <em>USB\\Vid_0000 & Pid_0000\\059B003112010E93</em>\\**デバイスパラメーター**

**アイコン**\[REG_MULTI_SZ\] =%*systemroo*t% *\\system32\\アイコン .ico*

**Nomediaicons** \[REG_MULTI_SZ\] =%*SystemRoot*% *\\system32\\noicon. .ico*

ドライバーまたはその他のコードは、**デバイスパラメーター**キーに直接アクセスしたり変更したりしないでください。 代わりに、次のシステム関数を使用する必要があります。

-   ユーザーモードでは、 [**Setupdicreatedevregkey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)と[**Setupdiopendevregkey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)を使用します。

-   カーネルモードの場合は、 [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)を使用します。

 

 






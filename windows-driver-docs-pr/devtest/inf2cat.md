---
title: Inf2Cat
description: Inf2Cat (Inf2Cat.exe) は、ドライバー パッケージの INF ファイルによって Windows のバージョンの指定されたリストのデジタル署名されたかどうかを決定するコマンド ライン ツール。
ms.assetid: 5d85058e-4051-4321-a4c1-b1a71d232b7f
keywords:
- Inf2Cat ドライバーの開発ツール
topic_type:
- apiref
api_name:
- Inf2Cat
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80739fb9c8226b4c35c4799f7881a9586bb47dc5
ms.sourcegitcommit: a58b4859254a651502e4329a6e521fe0fa11c7f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56582950"
---
# <a name="inf2cat"></a>Inf2Cat

Inf2Cat (Inf2Cat.exe) は、コマンド ライン ツールを決定するかどうかを[ドライバー パッケージの](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)INF ファイルは、Windows のバージョンの指定されたリストのデジタル署名することができます。 そのため、Inf2Cat を生成、署名されていない場合[カタログ ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)指定の Windows バージョンに適用します。

```command
    Inf2Cat /driver:
    PackagePath
     /os:
    WindowsVersionList [/nocat] [/verbose] [/?] [other switches]
```

> [!TIP]
> 表示された場合`DriverVer set to a date in the future`、ドライバーを作成するときに Inf2Cat を設定するため、ドライバー パッケージのプロジェクト設定を変更`/uselocaltime`します。 このためには、**[構成プロパティ] -> [Inf2Cat] -> [全般] -> [Use Local Time]\(現地時刻の使用\)** を使用します。 これで、[Stampinf](stampinf-command-options.md) と Inf2Cat の両方で現地時刻が使用されます。

Inf2Cat ツールが、プログラム ファイルにある\\Windows キット\\8.0\\bin\\x86 または Program Files (x86)\\Windows キット\\8.0\\bin\\x86WDK のフォルダーです。

## <a name="switches-and-arguments"></a>スイッチと引数

**/driver:**<em>PackagePath</em>  
ドライバー パッケージの INF ファイルを含むディレクトリへのパスを指定します。 指定したディレクトリに複数のドライバー パッケージ用の INF ファイルが含まれている Inf2Cat は各ドライバ パッケージのカタログ ファイルを作成します。

> [!NOTE]
> 使用することができます、 **/drv:** の代わりに切り替え、 **/driver:** スイッチします。

**/nocat**  
確認する Inf2Cat を構成、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)バージョンでは、指定した Windows の署名の要件に準拠しているが、ファイルのカタログを生成しないようにします。

**/os:**<em>WindowsVersionList</em>  
確認する Inf2Cat を構成、[ドライバー パッケージの](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)INF ファイルで指定されている Windows バージョンの署名の要件に準拠*WindowsVersionList*します。 *WindowsVersionList*はコンマ区切りの一覧で、次のバージョン識別子の 1 つ以上が含まれています。

|Windows のバージョン|バージョン識別子|
|--- |--- |
|Windows 10 x86 Edition|10_X86|
|Windows 10 x64 Edition|10_X64|
|Windows Server 2016|Server10_X64|
|ARM 上の Windows Server 2016|Server10_ARM64|
|Windows 8.1 x86 Edition|6_3_X86|
|Windows 8.1 x64 Edition|6_3_X64|
|Windows 8.1 の ARM エディション|6_3_ARM|
|Windows Server 2012 R2|Server6_3_X64|
|Windows 8 x64 Edition|8_X64|
|Windows 8 x86 Edition|8_X86|
|Windows 8 の ARM Edition|8_ARM|
|Windows Server 2012|Server8_X64|
|Windows Server 2008 R2 x64 Edition|Server2008R2_X64|
|Windows Server 2008 R2 の Itanium Edition|Server2008R2_IA64|
|Windows 7 x64 Edition|7_X64|
|Windows 7 x86 Edition|7_X86|
|Windows Server 2008 の x64 Edition|Server2008_X64|
|Windows Server 2008 の Itanium Edition|Server2008_IA64|
|Windows Server 2008 x86 Edition|Server2008_X86|

> [!NOTE]
> Windows Server 2008 R2 以降、Windows server オペレーティング システムは、x86 ベースのプラットフォームをサポートしません。

Inf2Cat は、バージョン識別子の文字列のアルファベット文字の大文字と小文字を無視します。 たとえば、vista\_x64、および Vista\_X64 は Windows Vista x64 Edition の両方の有効な識別子。

**/uselocaltime**  
ドライバーのタイムスタンプの検証テストの実行中にローカル タイム ゾーンを使用します。 既定で UTC が使用されます。

**/nocat**  
カタログの作成を禁止します。

**/verbose**  
コマンド ウィンドウに詳細な情報を表示する Inf2Cat を構成します。

**/?**  
コマンド ウィンドウでヘルプ情報を表示する Inf2Cat を構成します。

**/drm**  
*非推奨のコマンドライン引数です。*  
Drm 署名属性を追加する .inf ファイルでは、drm 署名属性を追加します。

**/pe**  
*非推奨のコマンドライン引数です。*  
Petrust 署名属性を追加する .inf ファイルで petrust シグネチャの属性を追加します。

**/pageHashes**  
ファイルにページ ハッシュを含めます。  必要に応じて、後にファイルの一覧が続きます。

## <a name="comments"></a>コメント

Inf2Cat ツールには、可否のツールのバージョンの Windows Vista より前に WDK に含まれているが置き換えられます。

Inf2Cat を使用するには、システムの Administrators グループのメンバーがあります。

確認が Inf2Cat ツール[ドライバー パッケージの](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)INF ファイルの構造化エラーとデジタル署名されたことができます、ドライバー パッケージであることを確認します。 すべての INF ファイルで参照されているファイルが存在して、ソース ファイルは、正しい位置にいる場合にのみ、ドライバー パッケージを署名できます。 場合は、INF ファイルを署名することはできません、または構造化エラーが含まれている場合は、ドライバー パッケージが正しくインストールされていない可能性があります。 またはドライバーのインストール中に警告 ダイアログ ボックスの署名が正しく表示します。

Inf2Cat を生成、[カタログ ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)カタログ ファイルは、ドライバー パッケージの INF ファイルで指定し、カタログ ファイルが 1 つ以上の指定された Windows バージョンに適用している場合にのみです。 場合、 [ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)の INF ファイルでのみは、 **CatalogFile =**<em>filename.cat</em>にディレクティブをそのカタログ ファイルを適用全体のドライバー パッケージです。 サポートするために[クロスプラット フォームのインストール](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)、INF ファイルを含める必要があります**CatalogFile** 。<em>PlatformExtension</em>**=**<em>一意 filename.cat</em>ディレクティブ。

ドライバー パッケージに署名に関する詳細については、次を参照してください。[ドライバーの署名](https://msdn.microsoft.com/library/windows/hardware/ff544865)と[デバイスとドライバーのインストールの基本的なトピック](https://msdn.microsoft.com/library/windows/hardware/ff541165)します。

## <a name="examples"></a>使用例

次の例では、c:\\MyDriver が含まれています、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)INF ファイルがある MyInfFile.inf と INF ファイルのバージョンの INF セクションには、次オプションのみにはが含まれています**CatalogFile** 。ディレクティブ。

```command
[Version]
. . .
CatalogFile=MyCatalogFile.cat
. . .
```

この例では、次の Inf2Cat コマンドによっては Windows Vista、Windows Server 2003、および Windows XP の Windows 2000 および x86 バージョンのドライバー パッケージを署名できるかどうかを確認します。 これらのバージョンのパッケージが署名することができる場合、Inf2Cat は MyCatalogFile.cat 符号なしのカタログ ファイルを作成します。

```command
Inf2Cat /driver:C:\MyDriver /os:2000,XP_X86,Server2003_X86,Vista_X86
```

次の例では、c:\\MyDriver が含まれています、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)の INF ファイルは MyInfFile.inf であり、INF**バージョン**INF ファイルのセクションには、次の 2 つのみが含まれています **。CatalogFile**ディレクティブをプラットフォーム拡張機能。

```command
[Version]
. . .
CatalogFile.ntx86=MyCatalogFileX86.cat
CatalogFile.ntamd64=MyCatalogFileX64.cat
. . .
```

次の Inf2Cat コマンドこの例では、Windows 2000 および x86 のドライバー パッケージを署名できるかどうかを確認は Windows Vista、Windows Server 2003、および Windows XP のバージョン。 さらに、コマンドがドライバー パッケージを x64 の場合、署名できるかどうかを確認すると Windows Vista、Windows Server 2003、および Windows XP のエディション。 これらのバージョンのすべてのパッケージが署名することができる場合、Inf2Cat は MyCatalogFileX86.cat および MyCatalogFileX64.cat 符号なしのカタログ ファイルを作成します。

```command
Inf2Cat /driver:C:\MyDriver /os:2000,XP_X86,XP_X64,Server2003_X86,Server2003_X64,Vista_X86,Vista_X64
```

Inf2Cat を使用して、カタログ ファイルを作成する方法の詳細については、次を参照してください。 [PnP ドライバー パッケージのカタログ ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers/install/creating-a-catalog-file-for-a-pnp-driver-package)します。

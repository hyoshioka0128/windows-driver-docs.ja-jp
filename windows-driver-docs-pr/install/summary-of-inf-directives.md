---
title: INF ディレクティブの概要
description: INF ディレクティブの概要
ms.assetid: 6212502c-183c-4abb-9e56-59dba15fc685
keywords:
- INF ファイル WDK デバイス インストールでは、ディレクティブ
- WDK の INF ファイルのディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e216d6ca081b008b602d13e80b7213eabb58150a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570105"
---
# <a name="summary-of-inf-directives"></a>INF ディレクティブの概要





多くを次に示します (ただしすべて) の INF ファイルで使用できるディレクティブ。 INF のディレクティブ名が、区別されます。 たとえば、 **Addreg**、 **addReg**、および**AddReg** INF ファイル内でのディレクティブの仕様と同様に有効です。

このセクションは、その逆方向または関連するディレクティブと共に最初に、最もよく使用されるディレクティブを示します。 使用頻度の最も低いディレクティブでは、リストの末尾に向かってです。

<a href="" id="addreg-directive"></a>[**AddReg ディレクティブ**](inf-addreg-directive.md)  
このディレクティブは、1 つまたは複数を参照*追加レジストリ セクション*で、これは INF セクションが追加またはサブキーを変更し、レジストリのエントリの値を使用します。

これで、特定の INF セクション、 **AddReg** (または**して**) ディレクティブが存在する、既定の参照先ので指定された変更を受信する相対的なレジストリの場所を決定します。*追加レジストリ セクション*(または*delete-section レジストリ*)。 これら既定のレジストリの場所は、特定のデバイスまたはドライバーに固有のサブキー HKEY_LOCAL_MACHINE レジストリ ツリーのどこかでは通常です。 詳細については、[レジストリ ツリーとデバイスとドライバーのキー](registry-trees-and-keys.md)を参照してください。

追加*追加レジストリ セクション*より高いレベルのドライバ、新しいデバイスのエクスポート (カーネル ストリーミング インターフェイス) などのデバイスのシステム定義のインターフェイスのベンダーから提供された共同インストーラーをレジストリ情報を設定できますデバイス ドライバーのサービスの特定のクラスに対して、インストールされているコンポーネントによってエクスポートされたインターフェイスまたは (ほとんど)、INF があるいる場合はデバイスの新しいセットアップ クラスに対する、 **ClassInstall32**セクション。

<a href="" id="delreg-directive"></a>[**してディレクティブ**](inf-delreg-directive.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

このディレクティブは、1 つまたは複数を参照*del-section レジストリ*廃止サブキーの削除や、レジストリからのエントリの値を使用します。 たとえば、このようなセクションは可能性があります、以前のインストールをアップグレードする INF に表示されます。

<a href="" id="copyfiles-directive"></a>[**CopyFiles ディレクティブ**](inf-copyfiles-directive.md)  
このディレクティブは、1 つまたは複数を参照*ファイルのセクション一覧*s 配布メディアからモデル/デバイス固有ドライバー イメージとその他の必要なファイルの各ファイルの保存先ディレクトリへの転送を指定します。 また、このディレクティブは、既定のインストール先ディレクトリに、配布メディアからコピーされる 1 つのファイルを指定できます。

<a href="" id="delfiles-directive"></a>[**DelFiles ディレクティブ**](inf-delfiles-directive.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

1 つまたは複数のディレクティブの参照を使用するほとんどありません*ファイルのセクション一覧*s が、インストールの対象から削除するファイルを指定します。

<a href="" id="renfiles-directive"></a>[**RenFiles ディレクティブ**](inf-renfiles-directive.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

1 つまたは複数のディレクティブの参照を使用するほとんどありません*ファイルのセクション一覧*の先に名前を変更する INF に関連付けられているソース ファイルを指定します。

<a href="" id="addservice-directive"></a>[**AddService ディレクティブ**](inf-addservice-directive.md)  
このディレクティブを参照して、少なくとも*サービス-インストール セクション*、追加された可能性がある*イベント ログ-インストール セクション*します。

ほとんどの種類 (ドライバーをインストールするもの) デバイスの INF ファイルは、INF ライターの定義がある*サービス-インストール セクション*システム提供のドライバーやサービスのどの段階で、システムのすべての依存関係を指定するには指定されたドライバーを読み込む必要があります、初期化プロセスとなどです。 デバイス ドライバーの INF ファイルが、INF ライターの定義があることも*イベント ログ-インストール セクション*によって参照される、 **AddService**ディレクティブをイベント ログ、デバイス ドライバーを設定します。

<a href="" id="delservice-directive"></a>[**DelService ディレクティブ**](inf-delservice-directive.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

使用頻度の低いこのディレクティブは、以前にインストールされたサービスを削除します。

<a href="" id="addinterface-directive"></a>[**AddInterface ディレクティブ**](inf-addinterface-directive.md)  
このディレクティブの参照、*追加インターフェイス セクション*を 1 つまたは複数**AddReg**でサポートされるデバイス インターフェイスのレジストリ エントリを設定するセクションを参照するディレクティブが指定されてこのデバイス/ドライバー。 必要に応じて、このような*追加インターフェイス セクション*delete レジストリ、ファイル転送、ファイルの削除、またはファイルの名前変更操作を指定する 1 つまたは複数の追加セクションを参照できます。

<a href="" id="bitreg-directive"></a>[**BitReg ディレクティブ**](inf-bitreg-directive.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

1 つまたは複数のディレクティブの参照を使用するほとんどありません*ビットのレジストリ セクション*既存を指定する s [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-値の特定のビットが変更するのには、レジストリにエントリの値を入力.

<a href="" id="logconfig-directive"></a>[**LogConfig ディレクティブ**](inf-logconfig-directive.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

このディレクティブは、1 つまたは複数を参照*ログの構成 セクションで*(PnP デバイスの列挙子) によって検出されたデバイスの場合、INF で許容されるバス相対、およびデバイスに固有のハードウェア構成を指定するか、手動でインストールされています。 たとえば、INF ファイルの非 PnP ISA、EISA と MCA デバイスは、手動でインストールされたこのディレクティブを使用します。 (また[ **INF DDInstall.LogConfigOverride セクション**](inf-ddinstall-logconfigoverride-section.md))。

<a href="" id="updateinis-directive"></a>[**UpdateInis ディレクティブ**](inf-updateinis-directive.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

1 つまたは複数のディレクティブの参照を使用するほとんどありません*update-section ini*s のインストール時に読み取られる指定された INI ファイルの部分を指定して、その INI ファイル内に 1 行ずつ変更を指定する可能性があります。

<a href="" id="updateinifields-directive"></a>[**UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

1 つまたは複数のディレクティブの参照を使用するほとんどありません*update-section inifields*s、INI ファイルの行を内のフィールドで行われる変更を指定します。

<a href="" id="ini2reg-directive"></a>[**Ini2Reg ディレクティブ**](inf-ini2reg-directive.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

1 つまたは複数のディレクティブの参照を使用するほとんどありません*セクション レジストリ ini*s の行またはレジストリに書き込まれる、INI ファイルのセクションを指定します。

セクションを上記のディレクティブのいずれかを指定できますが、システムが決定します。 各ディレクティブの基本的な形式は、たとえば、各セクションの参照の正式な構文に示されます。

```cpp
[DDInstall] | [DDInstall.HW] | [DDInstall.CoInstallers] | 
[ClassInstall32] | [ClassInstall32.ntx86] | [ClassInstall32.ntia64] | [ClassInstall32.ntamd64]

AddReg=add-registry-section[,add-registry-section] ...
```

このセクションの残りの部分では、正式な構文と名前付きセクションのシステム定義、標準の INF ライター定義のセクションでは、および、INF ファイルで指定できるディレクティブの意味について説明します。

 

 






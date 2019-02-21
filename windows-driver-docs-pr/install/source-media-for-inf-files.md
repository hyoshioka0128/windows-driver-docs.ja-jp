---
title: ソース メディアの INF ファイル
description: ソース メディアの INF ファイル
ms.assetid: b8bb7115-acac-4364-a205-16816c52fdb0
keywords:
- INF ファイルのソース メディアの WDK デバイス インストール
- メディア WDK INF ファイル
- ソース メディア WDK INF ファイル
- 多機能デバイス WDK INF ファイル
- 装飾の INF WDK
- INF ファイル WDK デバイスのインストールとは別に出荷
- 配布の INF ファイルの WDK
- WDK の INF ファイルを個別に配布
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b66da54bc9c78a39e7d99f2106a4e7de69f1dfa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556667"
---
# <a name="source-media-for-inf-files"></a>ソース メディアの INF ファイル





デバイス ファイルのソース メディアを指定するために使用する必要がありますメソッドは、かどうか、INF ファイルからの出荷とは別に、オペレーティング システムに依存または、オペレーティング システムに付属します。

### <a name="source-media-for-inf-files"></a>ソース メディアの INF ファイル

ドライバーの INF ファイルを使用して、ファイルの場所を指定する[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)と[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)セクション。 このような INF が含まれている場合**Include**と**必要がある**内のエントリ、 [ ***DDInstall*** ](inf-ddinstall-section.md)セクションの他の INF ファイルと、セクションを参照するこれらファイルとのセクションでは、可能な追加のソースの場所を指定できます。

場合は、INF **SourceDisksNames**と**SourceDisksFiles**セクションと いいえ**Include**エントリ、 **SourceDisksNames**と**SourceDisksFiles**すべて、元のメディアとカタログを除く、ドライバー パッケージ内のソース ファイルと INF ファイルのセクションでを一覧表示する必要があります。

カタログ ファイルは、INF ファイルと同じ場所にある必要があります。 カタログ ファイルを圧縮しない必要があります。 インストール メディアに複数のディスクが含まれている場合*すべてディスク上の INF とカタログ ファイルの個別のコピーを含める必要がある*します。 これは、INF とカタログ ファイルの全体のインストール中にアクセスできるようにする必要がありますし続けるためにです。

### <a name="source-media-and-inf-files-that-contain-include-and-needs-entries"></a>ソース メディアとが含まれている INF ファイルが含まれ、エントリを必要があります。

場合は、INF [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)と[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)セクションと**Include**と**必要がある**エントリ、Windows を使用して、メインの INF ファイルと含まれている INF ファイルのいずれかのソース メディアを探します。 ソース メディアとソース ファイルの場所を指定するときに、可能な限り正確に含まれるファイルで特に重要です。

次の図に示すような挿入の INF ファイルの階層構造を検討してください。

![含まれている inf ファイルの階層の例を示す図](images/inf-hier.png)

この図は、INF ファイルを示しています (*MyMfDevice.inf)* 多機能デバイスにします。 この INF ファイルには、システム提供が含まれています。 *Mf.inf*ファイル。 参照されているファイルをコピー元のソース メディアの Windows を検索すると*MyMfDevice.inf*、検索、 **SourceDisksFiles**セクション*MyMfDevice.inf*およびコピーするファイルを参照する INF ファイルが含まれています。 Windows 検索*MyMfDevice.inf*が、それが含まれている INF ファイルを検索する順序は保証されません。

装飾**SourceDisksFiles**のセクションでは非装飾のセクションよりも優先場合でも、 *INF セクションを装飾*インクルード ファイルにします。 たとえば、前の図に示すような INF ファイル場合*Mf.inf*が含まれています、 **\[SourceDisksFiles.x86\]** セクションと*MyMfDevice*.*inf*のみ、非装飾を含む**\[SourceDisksFiles\]**  セクションで、Windows を使用して、装飾のセクションから*Mf.inf*x86 をインストールするときは、1 つ目のコンピューター。 そのため、他の INF ファイルを含む、INF では、プラットフォーム拡張機能を使用するセクション名を含める必要があります。

通常、ベンダーから提供された INF は内のファイルの場所を指定する必要があります、[ドライバー パッケージ](driver-packages.md)と原因 Windows のファイルの場所に含まれている INF ファイルを検索するにはなりません。 つまり、INF ファイルをコピーする仕入先を指定する必要があります両方、 **SourceDisksNames**と**SourceDisksFiles**  セクションで、プラットフォームの拡張機能、およびこれらのセクションでこれらのセクションを修飾する必要があります直接、INF によってコピーされたすべてのファイルの情報を含める必要があります。

仕入先のファイル名には、ベンダー固有と潜在的なファイル名の競合を回避するために限り必要があります。

注意してください**Includes**エントリは、システム提供の INF ファイルを指定する場合にのみ使用できます。

使用して、もう 1 つの INF ファイルでセクションを使用する INF ファイル、 **Include**と**必要がある**エントリは、一貫性を維持するために、関連するセクションを使用する必要があります。 例では、INF ファイルは、「インストール」セクションを参照している場合、(*DDInstall*) ドライバーをインストールするには別の INF ファイルことを参照する必要があります、 [ **INF *DDInstall*します。サービス セクション**](inf-ddinstall-services-section.md)付随するサービスをインストールします。 このような INF ファイルには、次のセクションでは、可能性があります。

```cpp
[DDInstall]
Include = AnotherINFFile.inf
Needs = AnotherINFFileDDInstall

[DDInstall.Services]
Include = AnotherINFFile.inf
Needs = AnotherINFFileDDInstall.Services
```

指定しているセクションの各に注意してください、**必要がある**ディレクティブを指定する必要がありますも、 **Include**ディレクティブで同じ INF ファイルが指定された場合でも、 **Include**ディレクティブ他の場所で INF します。

 

 






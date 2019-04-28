---
title: INF DestinationDirs セクション
description: DestinationDirs セクションは、ターゲット先ディレクトリを指定またはすべてのディレクトリをコピー、削除、または、INF ファイルで別の場所の名前で参照されているファイルに対する操作の名前を変更します。
ms.assetid: fadebcb9-da4b-4daf-9e84-822447e5cb2a
keywords:
- INF DestinationDirs セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DestinationDirs Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e0df8123a9ab861b102b87e72d62d43f0eb7b6d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380744"
---
# <a name="inf-destinationdirs-section"></a>INF DestinationDirs セクション


A **DestinationDirs**セクションでは、ターゲットのインストール先ディレクトリを指定します。 または、すべてのディレクトリをコピー、削除、または、INF ファイルで別の場所の名前で参照されているファイルに対する操作の名前を変更します。

```ini
[DestinationDirs]

[DefaultDestDir=dirid[,subdir]] 
[file-list-section=dirid[,subdir]]... 
```

## <a name="entries"></a>エントリ


<a href="" id="defaultdestdir-dirid--subdir-"></a>**DefaultDestDir =**<em>dirid</em>\[**、**<em>subdir</em>\]  
すべてのコピー、削除、またはに明示的に示されていないファイルの名前変更操作の既定の出力先ディレクトリを指定します、*ファイルのセクション一覧*他のエントリは、ここで参照します。 ファイル操作常に発生ように、適切なディレクトリに、INF ファイルに次が含まれています。 **Include**と**必要がある**エントリは、既定の変換先ディレクトリを指定しないでください。 詳細については、「解説」を参照してください。

<a href="" id="file-list-section-dirid--subdir--------------"></a><em>file-list-section</em>**=**<em>dirid</em>\[**,**<em>subdir</em>\]\] ...   
INF ライター決定によって参照されるセクションの名前を指定します、 [ **CopyFiles**](inf-copyfiles-directive.md)、 [ **RenFiles**](inf-renfiles-directive.md)、または[ **DelFiles** ](inf-delfiles-directive.md)ディレクティブ INF ファイルで別の場所。 このようなエントリの場合、このセクションでは省略可能ですが、 **DefaultDestDir**エントリとこの INF で指定されたすべてのファイルのコピー操作がある同じのターゲット。 ただし、すべて*ファイルのセクション一覧*によって参照される、 **RenFiles**または**DelFiles** INF で別の場所ディレクティブがここに表示する必要があります。

<a href="" id="dirid"></a>*Dirid*  
名前付きの可能性がある、名前で参照されているファイルに対する操作のターゲット ディレクトリのディレクトリ識別子を指定します*ファイルのセクション一覧*INF の。 一般的に使用されるの一覧については*dirids*を参照してください[を使用して Dirids](using-dirids.md)します。

<a href="" id="subdir"></a>*subdir*  
サブディレクトリを指定します (で識別されたディレクトリの下で、存在する場合、そのパスの残りの部分と*dirid*) でのファイル操作のコピー先にする、指定された*ファイルのセクション一覧*。

<a name="remarks"></a>注釈
-------

**DestinationDirs**セクションが使用するすべての INF ファイルで必要な[ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)を参照するか、*ファイル リスト セクション*、かどうかを**CopyFiles**、 [ **DelFiles**](inf-delfiles-directive.md)、または[ **RenFiles** ](inf-renfiles-directive.md)ディレクティブ。

場合*Abc.inf*に含まれる別の INF ファイルからセクション*Def.inf*、両方の INF ファイルを含めると、 **DefaultDestDir**ファイルのコピー、ファイル名の変更、またはファイルの削除のエントリ操作では、Windows で指定されている既定の保存先ディレクトリに対応するすべてのファイル操作を実行します。 Def.inf で指定されている既定のインストール ディレクトリは無視されます*Abc.inf*します。

ファイル操作常に発生ように、適切なディレクトリに、INF ファイルに次が含まれています**Include**と**必要がある**エントリを含めないでください、 **DefaultDestDir** 。内のエントリを**DestinationDirs**セクション。 代わりに、このような INF ファイルを明示的に参照すべて、*ファイルのセクション一覧*名前によって指定される[ **CopyFiles**](inf-copyfiles-directive.md)、 [ **RenFiles**](inf-renfiles-directive.md)、および[ **DelFiles** ](inf-delfiles-directive.md)ディレクティブ、 **DestinationDirs**セクション。

INF ファイルが含まれていない場合**Include**と**必要がある**項目を INF を使用して、 **DefaultDestDir**コピーは、既定の出力先を指定するエントリの名前変更、およびファイルを削除INF ファイルの場所に表示される操作:

-   [**CopyFiles** ](inf-copyfiles-directive.md)直接コピーを使用するディレクティブ (@*filename*) 表記する必要がありますが、 **DefaultDestDir**内のエントリ、 **DestinationDirs**の INF を直接コピー エントリが表示されます。
-   **CopyFiles**、 [ **RenFiles**](inf-renfiles-directive.md)、または[ **DelFiles** ](inf-delfiles-directive.md)で直接参照されていないセクション、 **DestinationDirs**セクションがあります、 **DefaultDestDir**内のエントリ、 **DestinationDirs**のコピー、名前の変更、および削除ファイルのセクションを表示する INF セクション。

<a name="examples"></a>例
--------

この例では、すべてのファイルのコピー、削除、ファイル、およびファイルの名前の変更操作の既定のターゲット ディレクトリを設定します。 このような単純な**DestinationDirs**セクションは、このような INF は、ターゲット コンピューター上の 1 つのディレクトリにソース ファイルのセットをコピーする通常だけなので新しいの周辺機器の INF ファイルに共通します。

```ini
[DestinationDirs]
DefaultDestDir = 12 ; dirid = \Drivers on WinNT platforms
```

この例の一部を示して、 **DestinationDirs**の表示/ビデオ ドライバーの INF セクション。

```ini
[DestinationDirs]
DefaultDestDir     = 11 ; dirid = \system32 on WinNT platforms

; ... 

; list of per-Manufacturer, per-Models, per-DDInstall-section, and
; CopyFiles-referenced xxx.Miniport/xxx.Display sections omitted here
; along with several other miniport/display paired drivers
; ...
vga.Miniport     = 12
vga.Display      = 11
xga.Miniport     = 12
xga.Display      = 11

; all video miniports copied into \system32\drivers on WinNT platforms
; all paired display drivers copied into \system32
```

## <a name="see-also"></a>関連項目


[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**Dirids を使用します。**](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)

[**バージョン**](inf-version-section.md)

 

 







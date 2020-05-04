---
title: INF DestinationDirs セクション
description: DestinationDirs セクションでは、INF ファイル内の他の場所で参照されるファイルのすべてのコピー、削除、または名前変更操作の対象となるターゲットディレクトリを指定します。
ms.assetid: fadebcb9-da4b-4daf-9e84-822447e5cb2a
keywords:
- INF DestinationDirs セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DestinationDirs Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81c8c448a6f5c8d5aef5ce87fe965ec7deea8fb4
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223178"
---
# <a name="inf-destinationdirs-section"></a>INF DestinationDirs セクション


**Destinationdirs**セクションでは、INF ファイル内の他の場所で参照されるファイルのすべてのコピー、削除、または名前変更操作の対象となるターゲットディレクトリを指定します。

```inf
[DestinationDirs]

[DefaultDestDir=dirid[,subdir]] 
[file-list-section=dirid[,subdir]]... 
```

## <a name="entries"></a>エントリ


<a href="" id="defaultdestdir-dirid--subdir-"></a>**DefaultDestDir =**<em>dirid</em>\[**、**<em>subdir</em>\]  
他のエントリによって参照されるファイル*リストセクション*に明示的にリストされていないファイルに対するすべてのコピー、削除、または名前変更操作の既定の宛先ディレクトリをここに指定します。 ファイルの操作が常に正しいディレクトリで行われるようにするには、 **Include**エントリと**必要**なエントリを含む INF ファイルで、既定の保存先ディレクトリを指定しないでください。 詳細については、「解説」を参照してください。

<a href="" id="file-list-section-dirid--subdir--------------"></a><em>ファイルリストセクション</em>**=**<em>dirid</em>\[**,**<em>subdir</em> \] \] ...   
Inf ファイル内の別の場所にある、 [**CopyFiles**](inf-copyfiles-directive.md)、 [**RenFiles**](inf-renfiles-directive.md)、または[**delfiles**](inf-delfiles-directive.md)ディレクティブによって参照されるセクションの inf ライターによって決定される名前を指定します。 このセクションに**DefaultDestDir**エントリがあり、この INF に指定されているすべてのコピーファイル操作のターゲットが同一である場合、このエントリは省略可能です。 ただし、 **RenFiles**または**delfiles**ディレクティブによって参照されている INF 内の他の場所にある*ファイルリストセクション*は、ここに記載されている必要があります。

<a href="" id="dirid"></a>*dirid*  
名前によって参照されるファイルに対する操作用のターゲットディレクトリのディレクトリ識別子を指定します。これは、INF の名前付き*ファイルリストセクション*内で使用できます。 一般的に使用される*dirids*の一覧については、「 [Dirids の使用](using-dirids.md)」を参照してください。

<a href="" id="subdir"></a>*subdir*  
指定された*ファイルリストセクション*内のファイル操作の出力先となるサブディレクトリ ( *dirid*によって識別されるディレクトリの中にある場合は、そのパスの残りの部分) を指定します。

<a name="remarks"></a>解説
-------

**Destinationdirs**セクションは、Inf の[**copyfiles ディレクティブ**](inf-copyfiles-directive.md)を使用するか、または、 **copyfiles**、 [**delfiles**](inf-delfiles-directive.md)、または[**RenFiles**](inf-renfiles-directive.md)ディレクティブが指定されているかどうかにかかわらず、*ファイルリストセクション*を参照するすべての inf ファイルに必要です。

*Abc*に別の inf ファイルのセクションが含まれてい*て、両方*の inf ファイルにファイルのコピー、ファイル名の変更、またはファイルの削除操作の**DefaultDestDir**エントリが含まれている場合、Windows は、.def に指定されている既定の宛先ディレクトリを無視し、対応するすべてのファイル操作を、 *Abc*で指定されている既定の

ファイルの操作が常に正しいディレクトリで行われるようにするには、 **Include**エントリと**必要**なエントリを含む INF ファイルで**destinationdirs**セクションに**DefaultDestDir**エントリを含めないようにする必要があります。 代わりに、このような INF ファイルでは、 **Destinationdirs**セクションの[**CopyFiles**](inf-copyfiles-directive.md)、 [**RenFiles**](inf-renfiles-directive.md)、および[**delfiles**](inf-delfiles-directive.md)ディレクティブで指定されているすべての*ファイルリストセクション*名を明示的に参照する必要があります。

INF ファイルに**インクルード**および**必要**なエントリが含まれていない場合、inf は**DefaultDestDir**エントリを使用して、inf ファイル内の他の場所に表示されるコピー、名前の変更、およびファイルの削除操作の既定の宛先を指定できます。

-   直接コピー (@*filename*) 表記を使用する[**CopyFiles**](inf-copyfiles-directive.md)ディレクティブには、 **DefaultDestDir**エントリが INF の**destinationdirs**セクションに含まれている必要があります。このエントリは、直接コピーエントリが表示されます。
-   **Destinationdirs**セクションで直接参照されていない**CopyFiles**、 [**RenFiles**](inf-renfiles-directive.md)、または[**delfiles**](inf-delfiles-directive.md)の各セクションには、[コピー]、[名前の変更]、および [ファイルの削除] セクションが表示される INF の**destinationdirs**セクションに**DefaultDestDir**エントリが必要です。

<a name="examples"></a>例
--------

この例では、すべてのファイルのコピー、ファイルの削除、およびファイル名の変更操作の既定のターゲットディレクトリを設定します。 このような単純**Destinationdirs**セクションは、新しい周辺機器の inf ファイルに共通です。このような inf は通常、ソースファイルのセットをターゲットコンピューター上の単一のディレクトリにコピーするだけであるためです。

```inf
[DestinationDirs]
DefaultDestDir = 12 ; dirid = \Drivers on WinNT platforms
```

この例は、表示/ビデオドライバーの INF の**Destinationdirs**セクションのフラグメントを示しています。

```inf
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

[**Dirids の使用**](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)

[**バージョン**](inf-version-section.md)

 

 







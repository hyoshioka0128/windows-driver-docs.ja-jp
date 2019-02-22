---
title: INF SourceDisksFiles セクション
description: SourceDisksFiles セクション名はソース ファイル、インストール ディスク、およびインストール時に使用するディレクトリ パスです。
ms.assetid: 4a20b2e7-3371-47c1-8f51-bcc7af044382
keywords:
- INF SourceDisksFiles セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF SourceDisksFiles Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 410a84f32309842a2437d6c6fdd9572dd5b28b01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527692"
---
# <a name="inf-sourcedisksfiles-section"></a>INF SourceDisksFiles セクション


**SourceDisksFiles**セクションのインストール時に使用されるソース ファイルの名前、それらのファイルが含まれているインストール ディスクを識別およびを含むパッケージ内のディスクに存在する場合は、ディレクトリのパスを提供します個々 のファイル。

ドライバー ファイルまたはアプリケーション ファイルの署名の一部として含まれるため[ドライバー パッケージ](driver-packages.md)、ファイルは、対応する INF をいる必要があります**SourceDisksFiles**セクション エントリと対応する[ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)します。

```ini
[SourceDisksFiles] | 
[SourceDisksFiles.x86] | 
[SourceDisksFiles.arm] | (Windows 8 and later versions of Windows)
[SourceDisksFiles.arm64] | (Windows 10 version 1709 and later versions of Windows)
[SourceDisksFiles.ia64] | (Windows XP and later versions of Windows)
[SourceDisksFiles.amd64] (Windows XP and later versions of Windows)

filename=diskid[,[ subdir][,size]]
...  
```

## <a name="entries"></a>エントリ


<a href="" id="filename"></a>*ファイル名*  
ソース ディスク上のファイルの名前を指定します。

<a href="" id="diskid"></a>*ディスク id*  
ファイルを含むソースのディスクを識別する整数を指定します。 この値は、最初と*subdir*(ectory) パス (指定されている場合) を含む名前付きのファイルで定義する必要があります、 [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)の同じ INF セクション。

<a href="" id="subdir"></a>*subdir*  
この省略可能な値をサブディレクトリを指定します (を基準とする、*パス*の値、 **SourceDisksNames**セクションで、存在する場合)、名前付きのファイルがある、ソース ディスク上です。

名前付きのソース ファイルにあると想定エントリからこの値を省略した場合、*パス*で指定されたディレクトリ、 **SourceDisksFiles**特定のディスクのセクションまたは、ない場合は*パス*でディレクトリが指定されて、*インストール ルート*します。

<a href="" id="size"></a>*サイズ*  
この省略可能な値は、指定されたファイルのバイト単位で圧縮前のサイズを指定します。

<a name="remarks"></a>注釈
-------

A **SourceDisksFiles**セクションは、任意の数の配布のディスク上の各ファイルのエントリを持つことができます。 INF、 **SourceDisksFiles**セクションがあります、 [ **INF SourceDisksNames セクション**](inf-sourcedisksnames-section.md)します。 慣例により、 **SourceDisksNames**と**SourceDisksFiles**以下のセクションでは、 [ **INF バージョン セクション**](inf-version-section.md)します。 (これらのセクションでは、代わりを指定しますシステム提供の INF から省略、 **LayoutFile**エントリでその**バージョン**セクションです。)。

各*filename*エントリがソース ディスク上のファイルの正確な名前を指定する必要があります。 % を使用することはできません*strkey*% トークン ファイル名を指定します。 % の詳細については*strkey*% のトークンを参照してください[ **INF 文字列セクション**](inf-strings-section.md)します。

複数のシステム アーキテクチャにドライバー ファイルの配布をサポートするには、アーキテクチャ固有を指定できます**SourceDisksFiles**セクションを追加することで、 **.x86**、 **.ia64**、 **.amd64**、 **.arm**、または **.arm64**拡張機能を**SourceDisksFiles**します。 注意してくださいをなどの他のセクションとは異なり、 ***DDInstall***セクションで、プラットフォームの拡張機能、 **SourceDisksFiles**セクションがない **.ntx86**、**します。ntia64**、または **.ntamd64**します。

たとえば、ソース ディスク システムの x86 ベースのセクションの名前を指定するには、使用して、 **SourceDisksFiles.x86**セクションではなく、 **SourceDisksFiles.ntx86**セクション。 同様に、使用、 **SourceDisksFiles.ia64** 、Itanium ベース システムを指定するセクションと**SourceDisksFiles.amd64** x64 ベースのシステムを指定するセクション。

インストール中に、SetupAPI 関数の参照アーキテクチャに固有の**SourceDisksFiles**セクションでは、汎用のセクションを使用する前にします。 たとえばかどうかは、x86 ベースのプラットフォームでのインストール時に Windows がファイルをコピーするという*ルート*、ファイルの説明で検索されます **[SourceDisksFiles.x86]** で検索する前に **[SourceDisksFiles]**。

**重要な**  使用しないでください、 **SourceDisksFiles** INF ファイルをコピーするセクション。 INF ファイルをコピーする方法の詳細については、次を参照してください。[コピー Inf](copying-inf-files.md)します。

 

<a name="examples"></a>例
--------

次の例は、 [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)セクションと、対応する SourceDisksFiles セクション。  この例ではのみに注意してください、 **SourceDisksFiles.x86**  セクションで、x86 の場合、ファイルを指定するアーキテクチャです。  別のアーキテクチャをサポートする、INF は、対応する必要があります**SourceDisksFiles**そのアーキテクチャでは、または、非装飾の使用セクション **[SourceDisksFiles]** セクションで、すべての操作をサポートしていますアーキテクチャ。

```ini
[SourceDisksNames]
;
; diskid = description[, [tagfile] [, <unused>, subdir]]
;
1 = %Floppy_Description%,,,\WinNT

[SourceDisksFiles.x86]
aha154x.sys = 1,\x86 ; on distribution disk 1, in subdir \WinNT\x86

; ...
```

## <a name="see-also"></a>関連項目


[**CopyFiles、**](inf-copyfiles-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**バージョン**](inf-version-section.md)

 

 







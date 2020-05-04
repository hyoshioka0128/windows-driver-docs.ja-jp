---
title: INF SourceDisksFiles セクション
description: SourceDisksFiles セクションには、ソースファイル、インストールディスク、およびインストール時に使用されるディレクトリパスの名前が付いています。
ms.assetid: 4a20b2e7-3371-47c1-8f51-bcc7af044382
keywords:
- INF SourceDisksFiles セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF SourceDisksFiles Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e0f5dc83b15c522ac25546f773ad1cfdb1dca6f
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223206"
---
# <a name="inf-sourcedisksfiles-section"></a>INF SourceDisksFiles セクション


**Sourcedisksfiles**セクションは、インストール中に使用されるソースファイルの名前を指定し、それらのファイルが含まれているインストールディスクを識別します。また、個々のファイルを含むディストリビューションディスクにディレクトリパスがあれば、それらを提供します。

ドライバーファイルまたはアプリケーションファイルが署名付き[ドライバーパッケージ](driver-packages.md)の一部として含まれるようにするには、そのファイルに、対応する Inf **Sourcedisksfiles**セクションエントリと、対応する[**inf CopyFiles ディレクティブ**](inf-copyfiles-directive.md)が必要です。

```inf
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


<a href="" id="filename"></a>*/db*  
ソースディスク上のファイルの名前を指定します。

<a href="" id="diskid"></a>*diskid*  
ファイルが格納されているソースディスクを識別する整数を指定します。 この値は、名前付きファイルを含む最初の*subdir*(ectory) パスと共に、同じ INF の[**Sourcedisksnames**](inf-sourcedisksnames-section.md)セクションに定義されている必要があります。

<a href="" id="subdir"></a>*subdir*  
この省略可能な値は、名前付きファイルが存在するソースディスク上のサブディレクトリを指定します ( **Sourcedisksnames**セクションの*パス*値に対して相対的です)。

エントリからこの値を省略した場合、指定されたソースファイルは、指定されたディスクの**Sourcedisksfiles**セクションで指定された*パス*ディレクトリ、または*パス*ディレクトリが指定されていない場合は、*インストールルート*に存在すると見なされます。

<a href="" id="size"></a>*幅*  
この省略可能な値は、指定したファイルの圧縮されていないサイズ (バイト単位) を指定します。

<a name="remarks"></a>解説
-------

**Sourcedisksfiles**セクションには、ディストリビューションディスク上の各ファイルに1つずつ、任意の数のエントリを含めることができます。 **Sourcedisksfiles**セクションを含むすべての inf には、 [**Inf Sourcedisksfiles セクション**](inf-sourcedisksnames-section.md)も必要です。 慣例により、 **Sourcedisksnames**セクションと**Sourcedisksnames**セクションは、 [**「INF バージョン」セクション**](inf-version-section.md)に従います。 (これらのセクションは、システムによって提供されている INF には含まれていません。代わりに、**バージョン**セクションで**layoutfile**エントリが指定されます)。

各*ファイル名*エントリには、ソースディスク上のファイルの正確な名前を指定する必要があります。 %*Strkey*% トークンを使用してファイル名を指定することはできません。 %*Strkey*% トークンの詳細については、「 [**INF Strings」セクション**](inf-strings-section.md)を参照してください。

複数のシステムアーキテクチャでのドライバーファイルの配布をサポートするには、" **x86**"、" **ia64**"、" **amd64** **"、"** arm64"、または " **...** " の拡張子を**Sourcedisksfiles**に追加して、アーキテクチャ固有の**sourcedisksfiles**セクションを指定します。 ただし、 ***Ddinstall***セクションなどの他のセクションとは異なり、 **Sourcedisksfiles**セクションのプラットフォーム拡張機能は、 **ntx86**、 **. ntia64**、または**ntamd64**のいずれでもありません。

たとえば、x86 ベースのシステムの [ソースディスク名] セクションを指定するには、Sourcedisksfiles. **ntx86**セクションではなく、 **sourcedisksfiles. x86**セクションを使用します。 同様に、[ **Sourcedisksfiles. ia64** ] セクションを使用して、Itanium ベースのシステムと**sourcedisksfiles. amd64**セクションを指定し、x64 ベースのシステムを指定します。

インストール時に、Setupapi.log 関数は、ジェネリックセクションを使用する前に、アーキテクチャ固有の**Sourcedisksfiles**セクションを検索します。 たとえば、x86 ベースのプラットフォームにインストールしているときに、Windows が*driver*という名前のファイルをコピーする場合、[**sourcedisksfiles**] を調べる前に、[**sourcedisksfiles. x86**] でファイルの説明を検索します。

**重要**   **sourcedisksfiles**セクションを使用して INF ファイルをコピーしないでください。 INF ファイルをコピーする方法の詳細については、「 [inf のコピー](copying-inf-files.md)」を参照してください。

 

<a name="examples"></a>例
--------

次の例は、 [**Sourcedisksnames**](inf-sourcedisksnames-section.md)セクションと対応する Sourcedisksnames セクションを示しています。  この例には、x86 アーキテクチャ用のファイルを指定する**Sourcedisksfiles. x86**セクションのみが含まれています。  別のアーキテクチャをサポートする INF には、そのアーキテクチャに対応する**Sourcedisksfiles**セクション、またはすべてのアーキテクチャをサポートする、装飾されていない [**sourcedisksfiles**] セクションが必要です。

```inf
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


[**CopyFiles**](inf-copyfiles-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**バージョン**](inf-version-section.md)

 

 







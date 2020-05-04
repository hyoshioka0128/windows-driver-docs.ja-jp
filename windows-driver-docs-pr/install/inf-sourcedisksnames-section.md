---
title: INF SourceDisksNames セクション
description: SourceDisksNames セクションは、インストール中に対象のコンピュータに転送されるソースファイルが含まれているディストリビューションディスクまたは CD-ROM ディスクを識別します。
ms.assetid: ad69521c-5185-4c7b-a851-eb825b468459
keywords:
- INF SourceDisksNames セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF SourceDisksNames Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e4fa0833de5d1d3cda64edf98449c0260f3d9e5
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223204"
---
# <a name="inf-sourcedisksnames-section"></a>INF SourceDisksNames セクション


**Sourcedisksnames**セクションは、インストール中に対象のコンピュータに転送されるソースファイルが含まれているディストリビューションディスクまたは cd-rom ディスクを識別します。

```inf
[SourceDisksNames] |
[SourceDisksNames.x86] | 
[SourceDisksNames.arm] | (Windows 8 and later versions of Windows)
[SourceDisksNames.arm64] | (Windows 10 version 1709 and later versions of Windows)
[SourceDisksNames.ia64] | (Windows XP and later versions of Windows)
[SourceDisksNames.amd64] (Windows XP and later versions of Windows)

diskid = disk-description[,tag-or-cab-file] |
diskid = disk-description[,[tag-or-cab-file][,[unused][,path]]] |
diskid = disk-description[,[tag-or-cab-file],[unused],[path][,flags]] |
diskid = disk-description[,[tag-or-cab-file],[unused],[path],[flags][,tag-file]]  (Windows XP and later versions of Windows)
...
```

## <a name="entries"></a>エントリ


<a href="" id="diskid"></a>*diskid*  
ソースディスクを識別する負でない整数を10進数形式で指定します。 この値には、4バイトを超えるストレージは必要ありません。 ディストリビューション用に複数のソースディスクがある場合、このセクションの各*diskid*エントリには、 **1**、 **2**、 **3**などの一意の値を指定する必要があります。

<a href="" id="disk-description"></a>*ディスク-説明*  
*Diskid*によって識別されるディスクの内容や目的を説明する%*strkey*% トークンまたは **"**<em>引用符で囲ま</em>れた文字列 **"** を指定します。 インストーラーは、インストール中にこの文字列の値をエンドユーザーに表示できます。たとえば、インストールプロセスの特定の段階でドライブに挿入されるソースディスクを識別します。

このセクションの%*strkey*% 仕様は、すべて INF の**文字列**セクションで定義する必要があります。 %*Strkey*% トークンではない*ディスク記述*は、ユーザーが参照できる文字列で、先頭または末尾にスペースが含まれている場合は、二重引用符文字 (**"**) で区切る必要があります。

<a href="" id="tag-or-cab-file"></a>*タグまたは cab ファイル*  
このオプションの値は、配布ディスクに指定されている*タグファイル*または*キャビネット (.cab) ファイル*の名前を指定します。これは、*インストールルート*、または*パス*で指定されたサブディレクトリ (存在する場合) のいずれかになります。 値には、ディレクトリまたはサブディレクトリではなく、ファイル名と拡張子のみを指定する必要があります。

Windows では、ユーザーが適切なインストールディスクを挿入したことを確認するためにタグファイルを使用します。 タグファイルはリムーバブルメディアに必要であり、固定メディアでは省略可能です。

Windows がインストールメディアの名前でインストールファイルを見つけることができない場合、および*タグまたは cab ファイル*の拡張子がの場合 **。** Windows<em>では</em>、インストールファイルを含むキャビネットファイルの名前として使用されます。

の場合は。*cab*拡張が指定されている場合、Windows は、次の「**解説**」で説明するように、ファイルをタグファイルとキャビネットファイルの両方として扱います。

Windows XP 以降のバージョンの Windows では、*フラグ*と*タグファイル*のエントリ値も参照してください。

<a href="" id="unused"></a>*未使用*  
このエントリは、windows 2000 以降のバージョンの Windows ではサポートされなくなりました。

<a href="" id="path"></a>*道*  
このオプションの値は、ソースファイルを含むディストリビューションディスク上のディレクトリパスを指定します。 *パス*は*インストールルート*に対して相対的で、 **\\** <em>dirname1</em>**\\**<em>dirname2</em>として表現されます。などです。 エントリからこの値を省略した場合、ファイルは、配布ディスクのインストールルートに存在すると見なされます。

**INF SourceDisksFiles セクション**は、指定されたパスディレクトリまたはインストールルートに存在している必要があります。

<a href="" id="flags"></a>*示す*  
Windows XP 以降では、これを**0x10**に設定すると、windows によって、*タグまたは cab ファイルが*キャビネットファイル名として使用され、タグファイル名として*タグファイル*が使用されるようになります。 それ以外の場合、*フラグ*は内部でのみ使用されます。

<a href="" id="tag-file"></a>*タグファイル*  
Windows XP 以降では、 *flags*が**0x10**に設定されている場合、この省略可能な値は、配布メディアで指定された*インストールルート*または*パス*によって指定されたサブディレクトリにある*タグファイル*の名前を指定します。 値には、パス情報のないファイル名と拡張子を指定する必要があります。 詳細については、「解説」を参照してください。

<a name="remarks"></a>解説
-------

**Sourcedisksnames**セクションには、各ディストリビューションディスクに1つずつ、任意の数のエントリを含めることができます。 **Sourcedisksnames**セクションを含むすべての inf には、 [**Inf Sourcedisksnames セクション**](inf-sourcedisksfiles-section.md)も必要です。 (慣例により、 **Sourcedisksnames**セクションと**Sourcedisksnames**セクションは、 [**「INF バージョン」セクション**](inf-version-section.md)に従います)。

これらのセクションは、システムが提供する INF ファイルには表示されません。 システムが提供する INF ファイルでは、その**バージョン**セクションに**layoutfile**エントリが指定されています。

**Sourcedisksnames**セクション内のエントリは、2つの形式のいずれかを持つことができます。1つは windows XP 以降のバージョンの windows でのみサポートされています。

最初の形式では、*タグまたは cab*ファイルのパラメーターで、*タグファイル*または*キャビネットファイル*のいずれかを指定できます。 この形式が検出されると、Windows は次のアルゴリズムを使用します。

1.  *タグまたは cab ファイル*の値をタグファイル名として扱い、インストールメディアでファイルを検索します。 メディアがリムーバブルで、タグファイルが見つからない場合は、ユーザーに正しいメディアの入力を求めます。 メディアが固定されていて、インストールするタグファイルと最初のファイルのどちらも見つからない場合は、ユーザーに正しいメディアの入力を求めます。
2.  インストールファイルをメディアから直接コピーしようとしています。
3.  *タグまたは cab ファイル*の値を .cab ファイルとして扱い、ファイルを検索します。
4.  *.Cab*ファイルからインストールファイルをコピーしようとしています。
5.  ユーザーにファイルが見つからないことを確認するメッセージが表示されます。

2番目の形式は、windows XP 以降のバージョンの Windows でサポートされています。 この形式を使用すると、*タグファイルまたは cab*ファイル*のエントリを*使用し*て、* *.cab*ファイルとタグファイルの両方を指定できます。 この形式が検出されると、Windows は次のアルゴリズムを使用します。

1.  インストールメディアがリムーバブルの場合は、*タグ*ファイルで指定されたファイル名と一致するタグファイルを探します。 ファイルが見つからない場合は、ユーザーに正しいメディアの入力を求めます。 メディアが固定されている場合は、タグファイルまたはキャビネットファイルのいずれかを探します。 どちらのファイルも見つからない場合は、ユーザーに正しいメディアの入力を求めます。
2.  *タグまたは cab ファイル*によって指定された *.cab*ファイルからインストールファイルをコピーしようとしています。
3.  ユーザーにファイルが見つからないことを確認するメッセージが表示されます。

どちらの形式でも、ドライバーファイルのバージョンごとに異なるファイル名を持つ別のタグファイルを指定する必要があります。

複数のシステムアーキテクチャでのドライバーファイルの配布をサポートするには、ソース、 **ia64**、または**Amd64**拡張子を**sourcedisksnames**に追加して、アーキテクチャ固有の**sourcedisksnames**セクションを指定**します。**

*Ddinstall*セクションなどの他のセクションとは異なり、 **Sourcedisksnames**セクションのプラットフォーム拡張機能には、 **ntx86**、 **. ntia64**、または**ntamd64**は使用できません。 たとえば、x86 ベースのシステムに対して [source disk names] セクションを指定するには、sourcedisksnames. **ntx86**セクションではなく、 **sourcedisksnames. x86**セクションを使用します。 同様に、[ **Sourcedisksnames. ia64** ] セクションを使用して、Itanium ベースのシステムと**sourcedisksnames. amd64**セクションを指定し、x64 ベースのシステムを指定します。

インストール時に、Setupapi.log 関数は、ジェネリックセクションを使用する前に、アーキテクチャ固有の**Sourcedisksnames**セクションを検索します。 たとえば、x86 ベースのプラットフォームへのインストール中に INF ファイルがディスク "2" を参照している場合[、そのソースでは、](setupapi.md)ソースでディスク "2" のエントリが検索されてから**sourcedisksnames**が検索され**ます。**

Setupapi.log 関数は、 **sourcedisksnames**と**sourcedisksnames**を使用します。関連する[**Sourcedisksfiles**](inf-sourcedisksfiles-section.md)セクションと同じ INF ファイルにある<em>アーキテクチャ</em>セクション。

<a name="examples"></a>例
--------

次の例では、*書き込み .exe*ファイルはすべての Windows プラットフォームで同じであり、 * \\共通*のサブディレクトリ (インストールルートの下) にある cd-rom 配布ディスクにあります。*Cmd.exe*ファイルは、x86 ベースのプラットフォームでのみ使用されるプラットフォーム固有のファイルです。

```inf
[SourceDisksNames]
1 = "Windows NT CD-ROM",file.tag,,\common

[SourceDisksNames.x86]
2 = "Windows NT CD-ROM",file.tag,,\x86

[SourceDisksFiles]
write.exe = 1
cmd.exe = 2
```

次の例では、*タグ*ファイルと *.cab*ファイルに対して個別の仕様を含むエントリを使用します。

```inf
[Version]
signature = "$Windows NT$"
Provider = %Msft%

[SourceDisksNames]
1 = "Dajava","Dajava.cab",,,0x10,"Dajava.tag"
2 = "Osc","Osc.cab",,,0x10,"OSC.tag"
3 = "Win","Win.cab",,,0x10,"Win.tag"
4 = "XMLDSO","XMLDSO.cab",,,0x10,"XMLDSO.tag"

[SourceDisksFiles]
ArrayBvr.class=1
BvrCallback.class=1
BvrsToRun.class=1
choice.osc=2
custom.osc=2
login.osc=2
mwcload.exe=3
mwcloadw.exe=3
mwclw32.dll=3
Atom.class=4
DTD.class=4
Entity.class=4
Entry.class=4

[DestinationDirs]
Test = 16430,InfTest    ; %SystemRoot%\System32

[DefaultInstall]
CopyFiles = Test

[Test]
ArrayBvr.class
mwcloadw.exe
Entity.class
custom.osc
BvrCallback.class
BvrsToRun.class
choice.osc
login.osc
mwcload.exe
mwclw32.dll
Atom.class
DTD.class
Entry.class

[Strings]
Msft = "Microsoft"
```

## <a name="see-also"></a>関連項目


[**DestinationDirs**](inf-destinationdirs-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**バージョン**](inf-version-section.md)

 

 







---
title: INF SourceDisksNames セクション
description: SourceDisksNames セクションでは、パッケージ内のディスクまたはインストール中に対象のコンピューターに転送するソース ファイルが含まれている CD-ROM のディスクを識別します。
ms.assetid: ad69521c-5185-4c7b-a851-eb825b468459
keywords:
- INF SourceDisksNames セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF SourceDisksNames Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8133d47f86875787083cb74c53bd20a019eb426a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577844"
---
# <a name="inf-sourcedisksnames-section"></a>INF SourceDisksNames セクション


A **SourceDisksNames**配布ディスクや CD-ROM のディスクのインストール時にターゲット コンピューターに転送するソース ファイルが含まれているセクションを識別します。

```ini
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


<a href="" id="diskid"></a>*ディスク id*  
ソース ディスクを識別する、10 進形式では、負以外の整数を指定します。 この値には、4 バイトを超えるストレージが必要なことはできません。 分布の 1 つ以上のソース ディスクがある場合は、各*diskid*このセクションのエントリでは、一意の値をなどが必要**1**、 **2**、 **3**となります。

<a href="" id="disk-description"></a>*ディスクの説明*  
% を指定します*strkey*% トークンまたは **"**<em>文字列を引用符で囲まれた</em>**"** 内容やで識別されるディスクの目的を説明します。*diskid*します。 インストーラーを表示できますこの文字列の値、エンドユーザーのインストール中になど、インストール プロセスの特定のステージで、ドライブに挿入されるソース ディスクを識別します。

すべて %*strkey*INF のではこのセクションでは % 仕様を定義する必要があります**文字列**セクション。 すべて*ディスク説明*はない %*strkey*% トークンがユーザーに表示される文字列を二重引用符文字で区切る必要があります (**"**)、先頭がある場合または末尾のスペース。

<a href="" id="tag-or-cab-file"></a>*タグ-または-cab-ファイル*  
この省略可能な値の名前を指定する、*タグ ファイル*または*キャビネット (.cab) ファイル*配布ディスクは、のいずれかで指定された、*インストール ルート*またはサブディレクトリ指定された*パス*、存在する場合。 値は、ファイル名のみと拡張機能、いない任意のディレクトリまたはサブディレクトリを指定する必要があります。

Windows では、タグ ファイルを使用して、ユーザーが正しいインストール ディスクを挿入することを確認します。 タグ ファイルでは、リムーバブル メディアの場合に必要なしは固定メディアの省略可能です。

Windows では、インストール メディア上の名前によってインストール ファイルが見つからない場合、*タグ-または-cab-ファイル*拡張子 **.**<em>cab</em>、Windows インストール ファイルが含まれているキャビネット ファイルの名前として使用します。

場合、します。*cab*拡張機能を指定すると、Windows が以下で説明したように、タグ ファイルのキャビネット ファイルの両方としてファイルを扱います**解説**セクション。

Windows XP と Windows の以降のバージョンでは、参照も、*フラグ*と*タグ ファイル*エントリの値。

<a href="" id="unused"></a>*未使用*  
このエントリは Windows 2000 と Windows の以降のバージョンはサポートされていません。

<a href="" id="path"></a>*パス*  
この省略可能な値は、ソース ファイルが格納されている配布ディスク上のディレクトリ パスを指定します。 *パス*が関連して、*インストール ルート*として表されます**\\** <em>dirname1</em>  **。\\**<em>ディレクトリ名 2</em>.など。 この値はエントリから省略すると、ファイルは配布ディスクのインストールのルートであると見なされます。

使用することができます、 **INF SourceDisksFiles セクション**で指定されたパスのディレクトリ、またはインストール ルート内に存在する必要があります。

<a href="" id="flags"></a>*フラグ*  
これを設定、Windows XP 以降**0x10**強制的に使用する Windows*タグ-または-cab-ファイル*キャビネット ファイル名として使用して*タグ ファイル*タグ ファイル名として。 それ以外の場合、*フラグ*は内部でのみ使用されます。

<a href="" id="tag-file"></a>*タグ ファイル*  
場合は、Windows XP 以降*フラグ*に設定されている**0x10**、この省略可能な値の名前を指定する、*タグ ファイル*でいずれか、配布中に指定した*インストール ルート*またはで指定されたサブディレクトリで*パス*します。 値には、ファイル名とパス情報がない拡張機能を指定する必要があります。 詳細については、「解説」を参照してください。

<a name="remarks"></a>コメント
-------

A **SourceDisksNames**セクションは、任意の数の配布のディスクごとに 1 つのエントリを持つことができます。 INF、 **SourceDisksNames**セクションがあります、 [ **INF SourceDisksFiles セクション**](inf-sourcedisksfiles-section.md)します。 (慣例として、 **SourceDisksNames**と**SourceDisksFiles**以下のセクションでは、 [ **INF バージョン セクション**](inf-version-section.md))。

これらのセクションでは、システム提供の INF ファイルに表示されません。 システム提供の INF ファイルの代わりに、指定**LayoutFile**内のエントリ、**バージョン**セクション。

内のエントリを**SourceDisksNames**セクションは、Windows の Windows XP でのみサポートされている以降のバージョンは、その 1 つ、2 つの形式のいずれかを持つことができます。

最初の形式で、*タグ-または--cab*パラメーターは、いずれかを指定できます、*タグ ファイル*または*キャビネット ファイル*します。 この形式が発生する場合、Windows は、次のアルゴリズムを使用します。

1.  処理、*タグ-または--cab*タグ ファイルの名前と値し、インストール メディア上のファイルを検索します。 メディアが取り外し可能、タグ ファイルが見つからない場合は、中程度の適切なユーザーを確認します。 メディアが固定されており、タグ ファイルもインストールする最初のファイルを参照して、中程度の適切なユーザーを確認します。
2.  メディアから直接インストール ファイルをコピーしようとしてください。
3.  処理、*タグ-または--cab* .cab ファイルとしての値し、ファイルを探します。
4.  インストール ファイルをコピーしようとしています、 *.cab*ファイル。
5.  見つからないファイルのユーザーを要求します。

2 番目の形式は、Windows XP および Windows の以降のバージョンでサポートされます。 この形式を使用することができます、*タグ-または-cab-ファイル*、*フラグ*、および*タグ ファイル*両方を指定するエントリを *.cab*ファイルとタグ ファイル。 この形式が発生する場合、Windows は、次のアルゴリズムを使用します。

1.  インストール メディアが取り外し可能場合、検索で指定されているファイル名と一致するタグ ファイル*タグ ファイル*します。 ファイルが見つからない場合は、中程度の適切なユーザーを要求します。 メディアが修正された場合は、タグ ファイルまたはキャビネット ファイルを探します。 どちらのファイルが見つかった場合は、中程度の正しいユーザーを確認します。
2.  インストール ファイルをコピーしようとしています、 *.cab*によって指定されたファイル*タグ-または-cab-ファイル*します。
3.  見つからないファイルのユーザーを要求します。

いずれかの形式のドライバー ファイルの各バージョン用の別のファイル名を別のタグ ファイルを提供する必要があります。

複数のシステム アーキテクチャにドライバー ファイルの配布をサポートするには、アーキテクチャ固有を指定できます**SourceDisksNames**セクションを追加することで、 **.x86**、 **.ia64**、または **.amd64**拡張機能を**SourceDisksNames**します。

注意してくださいをなどの他のセクションとは異なり、 *DDInstall*セクションで、プラットフォームの拡張機能、 **SourceDisksNames**セクションがない **.ntx86**、**します。ntia64**、または **.ntamd64**します。 たとえば、ソース ディスク システムの x86 ベースのセクションの名前を指定するには、使用して、 **SourceDisksNames.x86**セクションではなく、 **SourceDisksNames.ntx86**セクション。 同様に、使用、 **SourceDisksNames.ia64** 、Itanium ベース システムを指定するセクションと**SourceDisksNames.amd64** x64 ベースのシステムを指定するセクション。

インストール中に、SetupAPI 関数の参照アーキテクチャに固有の**SourceDisksNames**セクションでは、汎用のセクションを使用する前にします。 たとえば、x86 ベースのプラットフォームでのインストール時に、INF ファイルがディスク「2」を参照している場合、 [SetupAPI](setupapi.md)関数は、ディスク「2」のエントリをで表示される**SourceDisksNames.x86**で検索する前に**SourceDisksNames**します。

SetupAPI 関数の使用、 **SourceDisksNames**と**SourceDisksNames** 。<em>アーキテクチャ</em>ファイルと同じ INF 内にあるセクションでは、関連するとして[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)セクション。

<a name="examples"></a>使用例
--------

次の例では、 *write.exe*ファイルがインストールされているすべての Windows プラットフォームにある、 *\\共通*配布 cd-rom 上のインストールのルートの下のサブディレクトリ.*Cmd.exe*ファイルは、x86 ベースのプラットフォームでのみ使用されるプラットフォーム固有のファイル。

```ini
[SourceDisksNames]
1 = "Windows NT CD-ROM",file.tag,,\common

[SourceDisksNames.x86]
2 = "Windows NT CD-ROM",file.tag,,\x86

[SourceDisksFiles]
write.exe = 1
cmd.exe = 2
```

次のコードの例では、個別の仕様が含まれるエントリ *.tag*ファイルと *.cab*ファイル。

```ini
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

 

 







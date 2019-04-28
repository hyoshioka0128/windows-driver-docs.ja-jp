---
title: INF DelFiles ディレクティブ
description: DelFiles ディレクティブ、INF ファイルで別の場所の INF ライター定義のセクションを参照し、削除するファイルの一覧。
ms.assetid: e163f88f-e0ab-41e7-97df-49853ec0836f
keywords:
- INF DelFiles ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DelFiles Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca4df3872f33d49efb001c62d77b2a75008b241e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370664"
---
# <a name="inf-delfiles-directive"></a>INF DelFiles ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **DelFiles**ディレクティブ、INF ファイルで別の場所の INF ライター定義のセクションを参照し、セクションに対する操作のコンテキストで削除するファイルの一覧、参照元**DelFiles**ディレクティブを指定します。

```ini
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows) 
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows) 
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows) 


  
Delfiles=file-list-section[,file-list-section]... 
```

A **DelFiles**いずれかのセクションでは、正式な構文のステートメントに示すように、ディレクティブを指定することができます。 このディレクティブは、INF ライター定義の次のセクションの中でも指定できます。

-   追加のインターフェイスのセクションで参照されている、 [ **AddInterface** ](inf-addinterface-directive.md)ディレクティブで、 [ * **DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)セクション。
-   インストール-インターフェイスのセクションで参照されている、 [ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)セクション

セクションによって参照される各名前付き、 **DelFiles**ディレクティブは、次の形式の 1 つまたは複数のエントリ。

```ini
[file-list-section]
 
destination-file-name[,,,flag]
...
```

A*ファイルのセクション一覧*それぞれ別々 の行に任意の数のエントリを持つことができます。

## <a name="entries"></a>エントリ


<a href="" id="destination-file-name"></a>*destination-file-name*  
転送先から削除するファイルの名前を指定します。

記載されているファイルを指定しない、 [ **CopyFiles** ](inf-copyfiles-directive.md)ディレクティブ。 両方のファイルが表示されている場合、 **CopyFiles**-参照されていると、 **DelFiles**-セクションを参照し、ファイルが有効な署名付きのシステムに現在存在する、オペレーティング システムの最適化により除外する場合がありますコピー操作では、削除操作が実行します。 これが非常に高い*いない*のためのもので、どのような INF ライター。

**注**  % を使用することはできません*strkey*% トークンを変換先ファイル名のエントリを指定します。 % の詳細については*strkey*% のトークンを参照してください[ **INF 文字列セクション**](inf-strings-section.md)します。

 

<a href="" id="flag"></a>*フラグ*  
この省略可能な値は、次のいずれかを指定できますここで、または 10 進数値で示すように、16 進表記で表されます。

<a href="" id="0x00000001--delflg-in-use-"></a>**0x00000001** (DELFLG_IN_USE)  
インストール プロセス中に使用された後に可能性がある名前付きのファイルを削除します。

この INF の処理中に使用されているために、指定されたファイルを削除できない場合、システムが再起動されるまで、ファイルの削除操作のキューを値、INF でこのフラグを設定します。 それ以外の場合、このようなファイルは削除されません。

<a href="" id="0x00010000---delflg-in-use1-"></a>**0x00010000** (DELFLG_IN_USE1)  
(Windows 2000 または Windows の以降のバージョン)このフラグは、DELFLG_IN_USE フラグの高い word バージョンであり、同じ目的と効果があります。 このフラグは、NT ベースのシステムでのインストールについてのみで使用する必要があります。

このフラグを設定、INF の値は両方と、INF で COPYFLG_WARN_IF_SKIP フラグと競合ができなくなります**DelFiles**と[ **CopyFiles** ](inf-copyfiles-directive.md)を参照するディレクティブ、同じ*ファイルのセクション一覧*します。

<a name="remarks"></a>コメント
-------

**重要な**  このディレクティブを慎重に使用する必要があります。 使用しないことを強くお勧め、 **DelFiles**プラグ アンド プレイの INF ファイルでディレクティブ (PnP) ドライバーに機能します。

 

すべて*ファイルのセクション一覧*名は、INF ファイルに固有である必要がありますが、それを参照できます[ **CopyFiles**](inf-copyfiles-directive.md)、 **DelFiles**、または[ **RenFiles** ](inf-renfiles-directive.md)他の場所で同じ INF ディレクティブ。 このような INF ライター定義セクション名は、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

**DelFiles**ディレクティブが修飾をサポートしていません、*ファイルのセクション一覧*システム定義のプラットフォームの拡張機能の名前 (**.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、または **.ntarm64**)。

[ **DestinationDirs** ](inf-destinationdirs-section.md) INF ファイルのセクションを含む特定のセクションに関係なく、すべてのファイルの削除操作の出力先を制御する**DelFiles**ディレクティブ。 場合によって参照される名前付きセクションを**DelFiles**ディレクティブ対応するエントリを持つ、 **DestinationDirs**同じ INF、そのエントリのセクションでは、ターゲット先のディレクトリから明示的に指定しますどの名前付きセクションに記載されているすべてのファイルは削除されます。 名前付きセクションが表示されていない場合、 **DestinationDirs**セクションで、Windows は、 **DefaultDestDir** INF 内のエントリ。

<a name="examples"></a>使用例
--------

この例では、どのように[ **DestinationDirs** ](inf-destinationdirs-section.md)セクションは、単純なデバイスのドライバーの INF の処理で行われるファイルの削除操作のパスを指定します。

```ini
[DestinationDirs]
DefaultDestDir = 12  ; DIRID_DRIVERS 

; ... 

[AHA154X]
CopyFiles=@AHA154x.MPD
DelFiles=ASPIDEV ; defines delete-files section name
; ... some other directives and sections omitted here

[ASPIDEV]
VASPID.SYS ; name of file to be deleted, if it exists on target 
; ...
```

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

**RenFiles**
[**文字列**](inf-strings-section.md)

 

 







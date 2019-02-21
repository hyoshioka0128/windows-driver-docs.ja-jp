---
title: INF RenFiles ディレクティブ
description: RenFiles ディレクティブは、他の場所に名前を変更するファイルの一覧を参照元 RenFiles ディレクティブが指定されているセクションに対する操作のコンテキストでは、INF ファイルでの INF ライター定義のセクションを参照します。
ms.assetid: 269171f7-88f6-47bb-9997-8fdcbe3fa688
keywords:
- INF RenFiles ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF RenFiles Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 091ef81745c7af19203f6d45dd16d0638a176193
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538896"
---
# <a name="inf-renfiles-directive"></a>INF RenFiles ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **RenFiles**ディレクティブが他の場所に名前を変更するファイルの一覧をセクションに対する操作のコンテキストでは、INF ファイルでの INF ライター定義のセクションを参照、参照元**RenFiles**ディレクティブを指定します。

```ini
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
Renfiles=file-list-section[,file-list-section]...
```

A **RenFiles**いずれかのセクションでは、正式な構文のステートメントに示すように、ディレクティブを指定することができます。 このディレクティブは、INF ライター定義の次のセクションの中でも指定できます。

-   *追加インターフェイス セクション*によって参照される、 [ **AddInterface** ](inf-addinterface-directive.md)ディレクティブで、 [ * **DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)セクション。
-   *インストール-section インターフェイス*で参照されている、 [ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)セクション。

セクションによって参照される各名前付き、 **RenFiles**ディレクティブは、次の形式の 1 つまたは複数のエントリ。

```ini
[file-list-section]
 
new-dest-file-name,old-source-file-name 
...
```

A*ファイルのセクション一覧*それぞれ別々 の行に任意の数のエントリを持つことができます。

## <a name="entries"></a>エントリ


<a href="" id="new-dest-file-name"></a>*new-dest-file-name*  
先にファイルに指定する新しい名前を指定します。

<a href="" id="old-source-file-name"></a>*古いソース ファイル名*  
ファイルの古い名前を指定します。

<a name="remarks"></a>注釈
-------

**重要な**  このディレクティブを慎重に使用する必要があります。 使用しないことを強くお勧め、 **RenFiles**プラグ アンド プレイの INF ファイルでディレクティブ (PnP) ドライバーに機能します。

 

すべて*ファイルのセクション一覧*名は、INF ファイルに固有である必要がありますが、それを参照できます[ **CopyFiles**](inf-copyfiles-directive.md)、 **DelFiles**、または**RenFiles**他の場所で同じ INF ディレクティブ。 このような INF ライター定義セクション名は、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

**RenFiles**ディレクティブが修飾をサポートしていません、*ファイルのセクション一覧*システム定義のプラットフォームの拡張機能の名前 (**.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、または **.ntarm64**)。

[ **DestinationDirs** ](inf-destinationdirs-section.md)をすべてファイル名の変更を含む特定のセクションに関係なく、操作、INF ファイルのセクションは、変換先を制御**RenFiles**ディレクティブ。 次の規則では、ファイルの名前変更操作について説明します。

-   場合によって参照される名前付きセクションを**RenFiles**ディレクティブ対応するエントリを持つ、 [ **DestinationDirs** ](inf-destinationdirs-section.md)エントリを明示的に指定する同じの INF セクション、ターゲットのインストール先ディレクトリ。 これらのソース ファイルがコピーされる前に、名前付きセクションに記載されているすべてのファイルが、先に変更されます。
-   名前付きセクションが表示されていない場合、 **DestinationDirs**セクションで、Windows は、 *DefaultDestDir*内のエントリ、 **DestinationDirs** INF のセクション。

**注**  % を使用することはできません*strkey*% トークンは、新しいまたは古いファイル名を指定します。 % の詳細については*strkey*% のトークンを参照してください[ **INF 文字列セクション**](inf-strings-section.md)します。

 

<a name="examples"></a>例
--------

この例で参照されているセクションを示しています、 **RenFiles**ディレクティブ。

```ini
[RenameOldFilesSec]
devfile41.sav, devfile41.sys
```

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

**DelFiles**
[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**バージョン**](inf-version-section.md)

 

 







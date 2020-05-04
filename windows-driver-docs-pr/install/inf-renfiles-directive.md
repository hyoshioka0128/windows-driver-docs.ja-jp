---
title: INF RenFiles ディレクティブ
description: RenFiles ディレクティブは、INF ファイル内の他の場所で INF ライターによって定義されたセクションを参照します。これにより、参照元の RenFiles ディレクティブが指定されているセクションで、操作のコンテキストでファイルの一覧の名前が変更されます。
ms.assetid: 269171f7-88f6-47bb-9997-8fdcbe3fa688
keywords:
- INF RenFiles ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF RenFiles Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf0cceb47cc656d0b8884241b0a24501b868fdd8
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223208"
---
# <a name="inf-renfiles-directive"></a>INF RenFiles ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**RenFiles**ディレクティブは、inf ファイル内の他の場所で inf ライターによって定義されたセクションを参照します。これにより、参照元の**RenFiles**ディレクティブが指定されているセクションで、操作のコンテキストでファイルの一覧の名前が変更されます。

```inf
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

**RenFiles**ディレクティブは、正式な構文ステートメントに示されている任意のセクション内で指定できます。 このディレクティブは、次のいずれかの INF ライターで定義されたセクション内で指定することもできます。

-   Ddinstall * で[**addinterface**](inf-addinterface-directive.md)ディレクティブによって参照される*インターフェイスセクション*。 [ *インターフェイス](inf-ddinstall-interfaces-section.md)セクション。
-   [**InterfaceInstall32**](inf-interfaceinstall32-section.md)セクションで参照される*インストールインターフェイスセクション*。

**RenFiles**ディレクティブによって参照される各名前付きセクションには、次の形式の1つ以上のエントリがあります。

```inf
[file-list-section]
 
new-dest-file-name,old-source-file-name 
...
```

*ファイルリストセクション*には任意の数のエントリを含めることができ、それぞれが個別の行に表示されます。

## <a name="entries"></a>エントリ


<a href="" id="new-dest-file-name"></a>*新しい-dest-ファイル名*  
転送先のファイルに指定する新しい名前を指定します。

<a href="" id="old-source-file-name"></a>*古い-ソース-ファイル名*  
ファイルの古い名前を指定します。

<a name="remarks"></a>解説
-------

**重要**  このディレクティブは、慎重に使用する必要があります。 プラグアンドプレイ (PnP) 関数ドライバーの INF ファイルでは、 **RenFiles**ディレクティブを使用しないことを強くお勧めします。

 

すべての*ファイルリストセクション*名は inf ファイルに対して一意である必要がありますが、同じ inf 内の他の場所では、 [**CopyFiles**](inf-copyfiles-directive.md)、 **Delfiles**、または**RenFiles**ディレクティブで参照できます。 このような INF ライターで定義されたセクション名は、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

**RenFiles**ディレクティブは、*ファイルリストセクション*名とシステム定義のプラットフォーム拡張機能 (**. nt**, **. ntx86**, **. ntia64**,. **ntamd64**, **. ntarm**,. **ntarm64**) を装飾することをサポートしていません。

INF ファイルの[**Destinationdirs**](inf-destinationdirs-section.md)セクションは、特定の**RenFiles**ディレクティブを含むセクションに関係なく、すべてのファイル名変更操作の対象を制御します。 次の規則は、ファイル名の変更操作を示しています。

-   **RenFiles**ディレクティブによって参照される名前付きセクションに、同じ INF の[**destinationdirs**](inf-destinationdirs-section.md)セクション内に対応するエントリがある場合、そのエントリはターゲットの宛先ディレクトリを明示的に指定します。 これらのソースファイルがコピーされる前に、名前付きセクションに示されているすべてのファイルの名前が変換先で変更されます。
-   **Destinationdirs**セクションに名前付きセクションが表示されていない場合、WINDOWS は INF の**Destinationdirs**セクションの*DefaultDestDir*エントリを使用します。

**メモ**  %*strkey*% トークンを使用して、新しいファイル名または古いファイル名を指定することはできません。 %*Strkey*% トークンの詳細については、「 [**INF Strings」セクション**](inf-strings-section.md)を参照してください。

 

<a name="examples"></a>例
--------

この例は、 **RenFiles**ディレクティブによって参照されるセクションを示しています。

```inf
[RenameOldFilesSec]
devfile41.sav, devfile41.sys
```

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

**Delfiles**
[**destinationdirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**バージョン**](inf-version-section.md)

 

 







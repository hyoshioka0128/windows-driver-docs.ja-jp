---
title: INF UpdateIniFields ディレクティブ
description: UpdateIniFields ディレクティブを INI ファイルの行を内の細かい変更を指定できます 1 つまたは複数の名前付きセクションを参照します。
ms.assetid: fda645c9-9ecb-46fe-9d21-1c042d56acd3
keywords:
- INF UpdateIniFields ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF UpdateIniFields Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a9b390b501f20d0d00c59c0c184da33b1e36cae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528209"
---
# <a name="inf-updateinifields-directive"></a>INF UpdateIniFields ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

**UpdateIniFields**ディレクティブは、INI ファイルの行を内の細かい変更を指定できます 1 つまたは複数の名前付きセクションを参照します。

```ini
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
UpdateIniFields=update-inifields-section[,update-inifields-section]...
```

セクションによって参照される各名前付き、 **UpdateIniFields**ディレクティブは、次の形式。

```ini
[update-inifields-section]
 
ini-file,ini-section,profile-name[,old-field][,new-field][,flags]
...
```

*Update-section inifields* INF ライター決定エントリの数をそれぞれ個別の行に持つことができます。

## <a name="entries"></a>エントリ


<a href="" id="ini-file"></a>*ini ファイル*  
ソース メディア、暗黙的に、あるターゲット コンピューターに更新される INI ファイルの指定された INI ファイルの名前を指定します。 としてこの値を表すことが、 *filename*または % として*strkey*% トークンで定義されている、 [**文字列**](inf-strings-section.md) INF ファイルのセクション。

<a href="" id="ini-section"></a>*ini セクション*  
変更する行を含む、指定された INI ファイル内のセクションの名前を指定します。

<a href="" id="profile-name"></a>*プロファイル名*  
指定された INI セクション内で変更する行の名前を指定します。 少なくとも 1 つの*old-field*や*新しいフィールド*この行の変更を有効にするためのエントリを指定する必要があります。

<a href="" id="old-field"></a>*old-field*  
指定した行内の既存のフィールドを指定します。 場合*新しいフィールド*を省略すると、その行からこのセクションのエントリからこのフィールドを削除します。 それ以外の場合、指定された*新しいフィールド*値は、このフィールドを置き換える必要があります。

<a href="" id="new-field"></a>*新しいフィールド*  
置換を指定します、特定*old-field*または、 *old-field*を省略すると、特定の行に追加します。

<a href="" id="flags"></a>*フラグ*  
(ビット 0) で指定されたを解釈する方法を指定します*古い*-*フィールド*や*新しい*-*フィールド*場合または両方にアスタリスクが含まれている (**\\**<em>)、(ビット 1) でどの区切り記号の文字を追加する場合に使用すると、指定された * 新しいフィールド</em>を次のように、特定の行に。

<a href="" id="bit-zero---0"></a>ビット 0 = **0**  
任意のアスタリスクを解釈 (\*)、指定した*old-field*や*新しいフィールド*エントリ文字どおり、INI ファイルの行内の特定の一致を検索するときに、ワイルドカード文字としてではなく。 これが既定値です。

<a href="" id="bit-zero---1"></a>ビット 0 = **1**  
任意のアスタリスクを解釈 (\*)、指定した*old-field*や*新しいフィールド*エントリを指定した行の INI ファイル内の一致を検索するときに、ワイルドカード文字として。

<a href="" id="bit-one---0"></a>ビット 1 = **0**  
指定した追加するときに、区切り記号として空白文字を使用して、*新しいフィールド*INI ファイルの特定の行に入力します。 これが既定値です。

<a href="" id="bit-one---1"></a>ビット 1 = **1**  
指定した追加するときに、区切り記号としてコンマ (,) を使用して、*新しいフィールド*INI ファイルの特定の行に入力します。

<a name="remarks"></a>注釈
-------

**UpdateIniFields**配布メディアに INI ファイルが存在するために必要ないため、Windows 上のインストール用の INF ファイルにディレクティブが指定されてほとんどありません。 ただし、 **UpdateIniFields**および INF ライター定義のセクションで参照されている正式な構文のステートメントで次のセクションのいずれかのディレクティブが正しく、 [ **AddInterface**](inf-addinterface-directive.md)ディレクティブまたはで参照されている、 [ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)セクション。

各*update-section inifields*名は、INF ファイルに一意である必要があります。 各 INF ライター作成セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)を参照してください。

によって参照されるセクションとは異なり、 [ **UpdateInis** ](inf-updateinis-directive.md)ディレクティブによって参照されるセクション、 **UpdateIniFields**置換、追加、または既存の INI ファイル内の行の部分を削除します。特定の行の値全体に影響を与えるのではなく行です。 少なくとも 1 つの*old-field*や*新しいフィールド*値は、各セクションのエントリで指定する必要があります。

INI ファイル変更される行のコメントは、それらが省かれるに従って、このセクションで変更した後にために削除されます。 INI ファイル内の行でフィールドを探すときに、スペース、タブ、およびコンマでは、フィールド区切り記号として解釈されます。 ただし、空白文字は、1 行に新しいフィールドが追加された場合、既定の区切り記号として使用されます。

完全なパスを提供する、INF、指定された*ini ファイル*配布メディアの次のいずれかの。

-   使用して、IHV と OEM 提供の INF ファイルで、 [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)と[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)にこの INF のセクションでは明示的に配布メディアのルート ディレクトリ (またはディレクトリ) ではない各名前付きのソース ファイルの完全なパスを指定します。
-   1 つまたは複数追加 INF ファイルで特定の指定した INF システムが指定したファイルの**LayoutFile**内のエントリ、 [**バージョン**](inf-version-section.md) INF ファイルのセクション。

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**バージョン**](inf-version-section.md)

 

 







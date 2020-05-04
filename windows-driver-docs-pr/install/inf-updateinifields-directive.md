---
title: INF UpdateIniFields ディレクティブ
description: UpdateIniFields ディレクティブは、1つまたは複数の名前付きセクションを参照します。このセクションでは、INI ファイルの行で細かい変更を指定できます。
ms.assetid: fda645c9-9ecb-46fe-9d21-1c042d56acd3
keywords:
- INF UpdateIniFields ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF UpdateIniFields Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9954df67dcb77de51b5dad19612fd5ae9d431ff
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223091"
---
# <a name="inf-updateinifields-directive"></a>INF UpdateIniFields ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**UpdateIniFields**ディレクティブは、1つまたは複数の名前付きセクションを参照します。このセクションでは、INI ファイルの行で細かい変更を指定できます。

```inf
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

**UpdateIniFields**ディレクティブによって参照される名前付きセクションには、次の形式があります。

```inf
[update-inifields-section]
 
ini-file,ini-section,profile-name[,old-field][,new-field][,flags]
...
```

*Inifields-セクション*には、任意の INF ライターが特定のエントリ数を指定できます。それぞれ個別の行に記述します。

## <a name="entries"></a>エントリ


<a href="" id="ini-file"></a>*ini-ファイル*  
ソースメディアで提供される INI ファイルの名前を指定します。これは、ターゲットコンピューター上の更新された INI ファイルの、暗黙的に指定されます。 この値は、*ファイル名*として、または INF ファイルの[**文字列**](inf-strings-section.md)セクションで定義されている%*strkey*% token として表すことができます。

<a href="" id="ini-section"></a>*ini-セクション*  
変更する行を含む、指定した INI ファイル内のセクションの名前を指定します。

<a href="" id="profile-name"></a>*プロファイル名*  
指定された INI セクション内で変更される行の名前を指定します。 この行の変更を反映するには、*古いフィールド*エントリまたは*新しいフィールド*エントリのうち少なくとも1つを指定する必要があります。

<a href="" id="old-field"></a>*old-フィールド*  
指定された行の既存のフィールドを指定します。 このセクションエントリから*新しいフィールド*を省略した場合、このフィールドは指定された行から削除されます。 それ以外の場合は、指定された*新しいフィールド*値でこのフィールドを置換する必要があります。

<a href="" id="new-field"></a>*新規-フィールド*  
指定された*古いフィールド*の置換を指定します。または、*古いフィールド*を省略した場合は、指定した行に追加します。

<a href="" id="flags"></a>*示す*  
指定された*古い*-*フィールド*や*新しい*-*フィールド*のいずれかまたは両方にアスタリスク () が含まれている場合**\\**、またはその両方にアスタリスク () が含まれている場合は、次のように、指定した * 新しいフィールドを指定の行に<em>追加するときに使用する区切り記号</em>をビット0で指定します。

<a href="" id="bit-zero---0"></a>ビットゼロ = **0**  
INI ファイルの指定\*された行で一致するものを検索するときに、指定した*古いフィールド*エントリまたは*新規フィールド*エントリのアスタリスク () を、ワイルドカード文字ではなく、リテラルとして解釈します。 これが既定値です。

<a href="" id="bit-zero---1"></a>ビットゼロ = **1**  
INI ファイルの指定\*した行で一致するものを検索するときに、指定した*古いフィールド*エントリまたは*新規フィールド*エントリのアスタリスク () をワイルドカード文字として解釈します。

<a href="" id="bit-one---0"></a>ビット 1 = **0**  
指定した*新しいフィールド*エントリを INI ファイルの指定した行に追加する場合は、区切り記号として空白文字を使用します。 これが既定値です。

<a href="" id="bit-one---1"></a>ビット 1 = **1**  
指定された*新しいフィールド*エントリを INI ファイルの指定された行に追加する場合は、区切り記号としてコンマ (,) を使用します。

<a name="remarks"></a>解説
-------

**UpdateIniFields**ディレクティブは、配布メディアに INI ファイルを配置する必要がないため、Windows でのインストールのために INF ファイルではほとんど指定されていません。 ただし、 **UpdateIniFields**ディレクティブは、 [**addinterface**](inf-addinterface-directive.md)ディレクティブによって参照されているか、 [**InterfaceInstall32**](inf-interfaceinstall32-section.md)セクションで参照されている INF ライターで定義されたセクションで、仮構文ステートメントに示されているいずれかのセクションで有効です。

*Inifields-セクション*名は、それぞれ INF ファイルに対して一意である必要があります。 各 INF ライターで作成されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

[**Updateinis**](inf-updateinis-directive.md)ディレクティブによって参照されるセクションとは異なり、 **UpdateIniFields**によって参照されるセクションでは、特定の行の値全体に影響を与えるのではなく、既存の INI ファイル行の行の部分が置換、追加、または削除されます。 *古いフィールド*値または*新しいフィールド*値の少なくとも1つを、各セクションエントリに指定する必要があります。

[変更後の INI ファイル] 行のコメントは、このセクションに従って変更を加えた後に適用されない可能性があるため、削除されます。 INI ファイル内の行のフィールドを検索する場合、スペース、タブ、およびコンマは、フィールド区切り記号として解釈されます。 ただし、新しいフィールドが行に追加されるときに、既定の区切り記号としてスペース文字が使用されます。

INF は、次のいずれかの方法で、配布メディアに指定された*ini ファイル*の完全なパスを提供します。

-   IHV/OEM が提供する INF ファイルで、この INF の[**Sourcedisksnames**](inf-sourcedisksnames-section.md)セクションと[**sourcedisksnames**](inf-sourcedisksfiles-section.md)セクションを使用して、配布メディアのルートディレクトリ (またはディレクトリ) にない各名前付きソースファイルの完全パスを明示的に指定します。
-   システムが提供する INF ファイルで、1つまたは複数の追加の INF ファイルを指定します。これは、INF ファイルの[**バージョン**](inf-version-section.md)セクションにある**layoutfile**エントリで確認できます。

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**バージョン**](inf-version-section.md)

 

 







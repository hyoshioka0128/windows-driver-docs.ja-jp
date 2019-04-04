---
title: INF UpdateInis ディレクティブ
description: UpdateInis ディレクティブでは、対象のコンピュータで同じ名前の既存の INI ファイルに適用する」セクションの読み取り元となる、INI ファイルを指定します。
ms.assetid: c4717b6c-dc2d-45ba-8b39-3fc33e49466e
keywords:
- INF UpdateInis ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF UpdateInis Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a67243a4c387317b5d5b60bab28915d27b52221d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578139"
---
# <a name="inf-updateinis-directive"></a>INF UpdateInis ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

**UpdateInis**ディレクティブが 1 つまたは複数の名前付きセクションで、INI ファイルを指定するを参照する特定のセクションまたは行があるが読み取られ、ターゲット コンピューターで同じ名前の既存の INI ファイルに適用します。 必要に応じて、1 行ずつ変更から、このような INI ファイルを指定できます、 *update-section ini*します。

```ini
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
UpdateInis=update-ini-section[,update-ini-section]...
```

INI ファイルの必要性がないのために、Windows のインストール用のファイルの INF では、このディレクティブは指定はほとんどありません。 ただし、 **UpdateInis**および INF ライター定義のセクションで参照されている正式な構文のステートメントで次のセクションのいずれかのディレクティブが正しく、 **AddInterface**ディレクティブまたは参照されている、 **InterfaceInstall32**セクション。

セクションによって参照される各名前付き、 **UpdateInis**ディレクティブは、次の形式。

```ini
[update-ini-section]
 
ini-file,ini-section[,old-ini-entry][,new-ini-entry][,flags]
...
```

*Update-section ini* INF ライター決定エントリの数をそれぞれ個別の行に持つことができます。

## <a name="entries"></a>エントリ


<a href="" id="ini-file"></a>*ini ファイル*  
ソース メディア、暗黙的に、あるターゲット コンピューターに更新する INI ファイルの指定された INI ファイルの名前を指定します。 としてこの値を表すことが、 *filename*または % として*strkey*% トークンで定義されている、 [**文字列**](inf-strings-section.md) INF ファイルのセクション。

<a href="" id="ini-section"></a>*ini セクション*  
指定された INI ファイル内のセクションの名前を指定します。 次の 2 つの値を指定する場合、このセクションには、エントリ変更するにはが含まれています。 場合、 *ini エントリの古い*を省略するしますが、*新しい ini エントリ*が指定されて、新しいエントリは、このセクションは読み取り専用として追加します。

<a href="" id="old-ini-entry"></a>*古い-entry ini*  
この省略可能な値内のエントリの名前を指定する、指定された*ini セクション*、通常は、次の形式で表されます。

```ini
"key=value"
```

いずれかまたは両方の*キー*と*値*% を表した*strkey*% のトークンで定義されている、**文字列**INF ファイルのセクション。 アスタリスク (**\\**<em>) のいずれか、ワイルドカードとして指定できる、* キー</em>または*値*します。

<a href="" id="new-ini-entry"></a>*new-ini-entry*  
この省略可能な値への変更を指定する、指定された*ini エントリの古い*や、新しいエントリの追加。 この値と同じ方法で表現できる*ini エントリの古い*します。

<a href="" id="flags"></a>*フラグ*  
この省略可能な値の解釈を制御する、指定された*ini エントリの古い*や*新しい ini エントリ*します。 *フラグ*エントリは、数値の値は次のいずれかを指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[値]</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>0</strong></td>
<td align="left"><p>これは、既定値、<em>フラグ</em>エントリを省略した場合。</p>
<p>場合、指定された<em>ini エントリの古い</em>キーは、INI ファイルに存在する、交換する<em>キー = 値</em>を指定した新しい-ini-エントリ。 INI ファイル内のキーのみが一致する必要があります。 このような各キーの対応する値は無視されます。</p>
<p>追加する、<em>新しい ini エントリ</em>無条件先 INI ファイルで、省略、 <em>ini エントリの古い</em>内のエントリの値、<em>更新 ini</em> INF のセクション。</p>
<p>無条件で移行先の INI ファイルから古い-ini-エントリを削除、省略、<em>新しい ini エントリ</em>値。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>1</strong></td>
<td align="left"><p>場合、指定された<em>ini エントリの古い</em>(<em>キー = 値</em>) が存在するを持つ移行先の INI ファイル内に置き換える、INI ファイルで、指定された<em>新しい ini エントリ</em>。 両方の<em>キー</em>と<em>値</em>の指定した<em>ini エントリの古い</em>の前の場合と、キーだけでなく、実現、このような交換は、INIファイルの一致する必要があります<em>フラグ</em>値。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>2</strong></td>
<td align="left"><p>場合、<em>キー</em>に指定されている<em>ini エントリの古い</em>変換先の INI ファイルを参照して、何もしないことはできません。 指定されたキーは、INI ファイルの一致に依存して行われた変更を検出するそれ以外の場合、 <em>ini エントリの古い</em>と<em>新しい ini エントリ</em>、次のようにします。</p>
<ol>
<li><p>場合、<em>キー</em>の<em>ini エントリの古い</em>INI ファイル内に存在するが、これは、<em>キー</em>の<em>新しい ini エントリ</em>、古い ini エントリを置き換える<em>新しい ini エントリ</em>先 INI ファイルし、その後、削除、余分な<em>新しい ini エントリ</em>INI ファイルから。</p></li>
<li><p>場合、<em>キー</em>の<em>ini エントリの古い</em>INI ファイル内のキーが存在する、<em>新しい ini エントリ</em>は、置換、 <em>ini エントリの古い</em>  <em>キー</em>のものと、<em>新しい ini エントリ</em>先 INI ファイルしますが、の値を受け入れ、 <em>ini エントリの古い</em>変更されません。</p></li>
</ol></td>
</tr>
<tr class="even">
<td align="left"><strong>3</strong></td>
<td align="left"><p>場合、<em>キー</em>と<em>値</em>向けに指定された<em>ini エントリの古い</em>INI ファイル、何もしないことはできません。 INI ファイルの一致に依存して行われた変更がそれ以外の場合、見つかった、指定された<em>キー</em>と<em>値</em>の<em>ini エントリの古い</em>と<em>新しい ini--entry</em>、次のようにします。</p>
<ol>
<li><p>場合、<em>キー = 値</em>の<em>ini エントリの古い</em>INI ファイル内に存在するが、これは、<em>キー = 値</em>の<em>新しい ini エントリ</em>、置換、<em>ini エントリの古い</em>で、<em>新しい ini エントリ</em>先 INI ファイルし、その後、削除、余分な<em>新しい ini エントリ</em>INI ファイルから。</p></li>
<li><p>場合、<em>キー = 値</em>の<em>ini エントリの古い</em>INI ファイル内に存在するが、<em>新しい ini エントリ</em>は、置換、 <em>ini エントリの古い</em><em>新しい ini エントリ</em>先 INI ファイルしますが、の値を受け入れ、 <em>ini エントリの古い</em>変更されません。</p></li>
</ol></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

指定された*update-section ini*名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)を参照してください。

完全なパスを提供する、INF、指定された*ini ファイル*配布メディアの次のいずれかの。

-   使用して、IHV と OEM 提供の INF ファイルで、 [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)と[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)にこの INF のセクションでは明示的に配布メディアのルート ディレクトリ (またはディレクトリ) ではない各名前付きのソース ファイルの完全なパスを指定します。
-   1 つまたは複数追加 INF ファイルで特定の指定した INF システムが指定したファイルの**LayoutFile**内のエントリ、 [**バージョン**](inf-version-section.md) INF ファイルのセクション。

すべて*filename*内で指定された、 *ini エントリの古い*または*新しい ini エントリ*ファイルを含む変換先のディレクトリを指定する必要があります。 このような変換先のディレクトリ パスを*ファイル名*で、 *update-section ini*としてエントリを指定する必要があります、 *dirid*します。 候補のリストの*dirid*値を参照してください[を使用して Dirids](using-dirids.md)します。

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**ProfileItems**](inf-profileitems-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**バージョン**](inf-version-section.md)

 

 







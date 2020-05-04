---
title: INF UpdateInis ディレクティブ
description: UpdateInis ディレクティブは、ターゲットコンピューター上の同じ名前の既存の INI ファイルに適用するセクションの読み取り元となる INI ファイルを指定します。
ms.assetid: c4717b6c-dc2d-45ba-8b39-3fc33e49466e
keywords:
- INF UpdateInis ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF UpdateInis Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e7cda0992c275158fea20bd3a0394e15375a23c
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223092"
---
# <a name="inf-updateinis-directive"></a>INF UpdateInis ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Updateinis**ディレクティブは、1つまたは複数の名前付きセクションを参照します。このとき、特定のセクションまたは行を読み取り、ターゲットコンピューター上の同じ名前の既存の ini ファイルに適用する ini ファイルを指定します。 必要に応じて、そのような INI ファイルからの行ごとの変更を、 *.ini セクション*で指定できます。

```inf
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

このディレクティブは、Windows にインストールするための INF ファイルではほとんど指定されていません。これは、INI ファイルの必要性がないためです。 ただし、 **Updateinis**ディレクティブは、仮構文ステートメントに示されているすべてのセクション、および**addinterface**ディレクティブによって参照されるか、 **InterfaceInstall32**セクションで参照されている INF ライターで定義されたセクションで有効です。

**Updateinis**ディレクティブによって参照される名前付きセクションには、次の形式があります。

```inf
[update-ini-section]
 
ini-file,ini-section[,old-ini-entry][,new-ini-entry][,flags]
...
```

*更新プログラムの .ini セクション*には、任意の数のエントリ (それぞれ別の行) を指定できます。

## <a name="entries"></a>エントリ


<a href="" id="ini-file"></a>*ini-ファイル*  
ソースメディアで提供される INI ファイルの名前を指定します。また、暗黙的に、ターゲットコンピュータ上で更新する INI ファイルの名前を指定します。 この値は、*ファイル名*として、または INF ファイルの[**文字列**](inf-strings-section.md)セクションで定義されている%*strkey*% token として表すことができます。

<a href="" id="ini-section"></a>*ini-セクション*  
指定された INI ファイル内のセクションの名前を指定します。 次の2つの値を指定した場合、このセクションには変更するエントリが含まれます。 *前の .ini エントリ*が省略されていても、*新しい ini*エントリが指定されている場合は、このセクションが読み取られたときに新しいエントリが追加されます。

<a href="" id="old-ini-entry"></a>*以前の ini エントリ*  
この省略可能な値は、指定された*ini セクション*内のエントリの名前を指定します。通常は、次の形式で表されます。

```inf
"key=value"
```

*キー*と*値*のどちらかまたは両方を、INF ファイルの**文字列**セクションで定義されている%*strkey*% token として表すことができます。 アスタリスク (**\\**) は、* キーまたは*値*の<em>いずれかのワイルドカードとして指定でき</em>ます。

<a href="" id="new-ini-entry"></a>*新しい .ini-エントリ*  
この省略可能な値は、指定した*前の ini エントリ*に対する変更、または新しいエントリの追加を指定します。 この値は、*前の ini エントリ*と同じ方法で表現できます。

<a href="" id="flags"></a>*示す*  
この省略可能な値は、指定された*旧バージョンの ini エントリ*または *.ini*エントリの解釈を制御します。 *Flags*エントリには、次の数値のいずれかを指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>0</strong></td>
<td align="left"><p>これは、<em>フラグ</em>エントリが省略されている場合の既定値です。</p>
<p>指定された<em>旧-ini エントリ</em>キーが ini ファイルに存在する場合は、その<em>キー = 値</em>を指定された新しい .ini エントリに置き換えます。 INI ファイル内のキーのみが一致している必要があります。 このようなキーの対応する値は無視されます。</p>
<p>コピー先の INI ファイルに無条件に<em>新しい .ini エントリ</em>を追加するには、INF の<em>.ini</em>セクションにあるエントリから、<em>以前の ini エントリ</em>の値を省略します。</p>
<p>コピー先の INI ファイルから前の ini エントリを無条件で削除するには、<em>新しい ini エントリ</em>の値を省略します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>1</strong></td>
<td align="left"><p>指定された<em>前の .ini エントリ</em>(<em>キー = 値</em>) が ini ファイルに存在する場合は、指定され<em>た .ini ファイル</em>のコピー先の ini ファイルで置き換えます。 前の<em>flags</em>値のキーだけでなく、指定した<em>旧バージョンの ini エントリ</em>のキーと<em>値</em>の両方が、ini ファイル内の<em>キー</em>と一致する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>2</strong></td>
<td align="left"><p>以前の ini<em>エントリ</em>に指定された<em>キー</em>がコピー先の ini ファイルに見つからない場合は、何もしません。 それ以外の場合、変更は、次のように、<em>以前の ini エントリ</em>と<em>.ini エントリ</em>の指定されたキーについて、ini ファイルで見つかった一致に依存します。</p>
<ol>
<li><p><em>旧バージョンの ini</em>エントリの<em>キー</em>が ini ファイルに存在していても、そのキーが .ini ファイルの<em>キー</em>である場合<em>は、以前</em>の ini エントリをコピー先の ini ファイルの<em>.ini エントリに</em>置き換えて、その ini ファイルから余分な<em>新しい ini エントリ</em>を削除します。</p></li>
<li><p><em>旧バージョンの ini</em>エントリの<em>キー</em>が ini ファイルに存在していても、<em>新しい ini</em>エントリのキーがではない場合は、<em>以前</em>の INI エントリの  <em>キー</em>をコピー先の ini ファイルの<em>.ini エントリ</em>のものに置き換えます。ただし、<em>以前の ini エントリ</em>の値は変更せずに残しておきます。</p></li>
</ol></td>
</tr>
<tr class="even">
<td align="left"><strong>3</strong></td>
<td align="left"><p><em>以前の ini エントリ</em>に指定された<em>キー</em>と<em>値</em>が ini ファイルに見つからない場合は、何もしません。 それ以外の変更は、次のように、指定された<em>キー</em>と、以前の<em>ini エントリ</em>と<em>新しい .ini エントリ</em>の<em>値</em>について、ini ファイルで見つかった一致に依存します。</p>
<ol>
<li><p><em>以前</em>の ini エントリの<em>キー = 値</em>が ini ファイルに存在するが、<em>新しい ini エントリ</em>の<em>キー = 値</em>を使用している場合は、<em>以前の ini エントリ</em>をコピー先の ini ファイルの<em>新しい .ini エントリ</em>に置き換え、その後、その ini ファイルから不要な<em>新しい ini</em>エントリを削除します。</p></li>
<li><p><em>以前</em>の ini エントリの<em>キー = 値</em>が ini ファイルに存在していても、<em>新しい ini</em>エントリには存在しない場合は<em>、以前の</em>ini エントリをコピー先の ini ファイルの<em>新しい .ini エントリ</em>に置き換えます。ただし、前の<em>ini エントリ</em>の値は変更せずに残しておきます。</p></li>
</ol></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

*.Ini セクション*名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

INF は、次のいずれかの方法で、配布メディアに指定された*ini ファイル*の完全なパスを提供します。

-   IHV/OEM が提供する INF ファイルで、この INF の[**Sourcedisksnames**](inf-sourcedisksnames-section.md)セクションと[**sourcedisksnames**](inf-sourcedisksfiles-section.md)セクションを使用して、配布メディアのルートディレクトリ (またはディレクトリ) にない各名前付きソースファイルの完全パスを明示的に指定します。
-   システムが提供する INF ファイルで、1つまたは複数の追加の INF ファイルを指定します。これは、INF ファイルの[**バージョン**](inf-version-section.md)セクションにある**layoutfile**エントリで確認できます。

*以前の ini エントリ*または*新しい .ini エントリ*内で指定されたファイル*名*は、そのファイルを含む宛先ディレクトリを指定する必要があります。 *.Ini セクション*エントリ内の*ファイル名*の保存先ディレクトリパスは、 *dirid*として指定する必要があります。 使用可能な*dirid*値の一覧については、「 [Dirid の使用](using-dirids.md)」を参照してください。

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**ProfileItems**](inf-profileitems-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**バージョン**](inf-version-section.md)

 

 







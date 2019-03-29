---
title: INF Strings セクション
description: INF ファイルをその INF で他の場所で指定されたすべての strkey トークンを定義する文字列 セクションには少なくとも 1 つがあります。
ms.assetid: 7352aa82-a7cd-4d15-9a9e-e03985f6006e
keywords:
- INF 文字列のセクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Strings Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d69c976faa7309f56d2b16344fd3d41c46ccb619
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348775"
---
# <a name="inf-strings-section"></a>INF Strings セクション


INF ファイルを少なくとも 1 つあります**文字列**すべて % を定義するセクション*strkey*その INF で他の場所で指定した % トークンです。

```ini
[Strings] | 
[Strings.LanguageID] ...
 
strkey1 = ["]some string["]
strkey2 = "    string-with-leading-or-trailing-whitespace     "  | 
          "very-long-multiline-string" | 
          "string-with-semicolon" | 
          "string-ending-in-backslash" |
          ""double-quoted-string-value""
 ...
```

## <a name="entries"></a>エントリ


<a href="" id="strkey1--strkey2-----"></a>*strkey1*, *strkey2*, ...  
INF ファイルでは、各文字列キーには、文字、数字、または明示的に表示されるその他の文字で構成される一意の名前を指定する必要があります。 内でこのような % 文字、 *strkey*としてトークンを表す必要があります **%%** します。

<a href="" id="some-string----some-string-"></a>*一部の文字列* | **"**<em>一部の文字列</em>**"**  
必要に応じて二重引用符文字 (")、具体的には英字、数字、句読点、および暗黙的に表示されるも可能性がある特定の文字が含まれていますが、内部のスペースやタブ文字を使用して区切り、文字列を指定します。 ただし、内部の二重引用符記号 (")、セミコロン (;)、改行、戻るとき、または非表示の制御文字、引用符なしの文字列を含めることはできませんし、円記号を含めることはできません (\)その最後の文字として。

<a href="" id="------string-with-leading-or-trailing-whitespace-----------"></a>**"***     string-with-leading-or-trailing-whitespace*     **"** |   

<a href="" id="-very-long-multiline-string----"></a>**"**<em>very-long-multiline-string</em>**"** |   

<a href="" id="-string-with-semicolon----"></a>**"**<em>string-with-semicolon</em>**"** |   

<a href="" id="-string-ending-in-backslash---"></a>**"**<em>string-ending-in-backslash</em>**"** |  

<a href="" id="--double-quoted-string-value--"></a>**"***"double-quoted-string-value"***"**  
% に指定された値*strkey*% トークン*する必要があります*囲む二重引用符 (") で、次の条件を満たしている場合。

-   指定した文字列にその値の一部として保持する必要があります、先頭または末尾の空白文字がある場合は、その文字列を先頭または末尾の空白文字が INF パーサーによって破棄されることを防ぐために二重引用符文字で囲む必要があります。
-   長い文字列は、テキスト エディターで行の折り返しのため内部改行または戻り値の文字に含まれて可能性があります、初期の内部改行時に文字列の切り捨てを防止または文字を返すには、二重引用符で囲むもする必要があります。
-   そのような文字列にセミコロンが含まれている場合は、文字列のセミコロンの位置の切り捨てを防ぐために二重引用符で囲む必要があります。 (で説明したように[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)、セミコロン文字は、各コメント INF ファイルを開始します)。
-   円記号は、このような文字列が終了した場合は、文字列が次のエントリと連結されていることを防ぐために二重引用符で囲む必要があります。 (前述の既に一般構文規則 INF ファイルの場合、円記号 (\) INF ファイルで行 continuator として使用されます)。
-   など、引用符なしの文字列の仕様では、このような「引用符で囲まれた文字列」内部の二重引用符文字を含めることはできません。 ただし、二重引用符文字 (たとえば、「"一部の文字列」") の 1 つまたは複数の他のペアを使用して明示的に二重引用符付き文字列値として指定することができます。

    INF パーサーでは、外側のこのセクションで、「引用符で囲まれた文字列」の二重引用符最も外側の組を破棄するだけでなくも 1 つの二重引用符文字を二重引用符の各後続のシーケンシャル ペアでまとめます。

    たとえば、「""一部の文字列」""にもなります「一部の文字列」が解析されます。

要約するは、任意の文字列は、次のいずれかが true の場合も、1 組の二重引用符文字 (") で囲む必要があります。

-   文字列には、先頭または末尾の空白文字が含まれています。
-   文字列は、行が時間の長いをラップするためです。
-   文字列には、セミコロンまたは最後の円記号の文字が含まれています。
-   文字列自体は、引用符で囲まれた文字列です。

システム INF パーサーでは、引用符の文字を二重引用符の文字列の区切り記号の外側の先頭または末尾にある空白文字と共に、このような文字列を区切る倍精度浮動小数点の最も外側の外側の組を破棄します。

<a name="remarks"></a>コメント
-------

システム INF パーサーが外側のいずれかからは、二重引用符最も外側の組によって削除されるため **"**<em>文字列を引用符で囲まれた</em>**"** % を定義する*strkey*システム INF ファイルの多く % トークン定義すべて %*strkey*% のトークンとして **"**<em>文字列を引用符で囲まれた</em><strong>"</strong>を回避します。先頭と末尾の空白文字の INF の解析中に予期しない損失。 使用 **"**<em>文字列を引用符で囲まれた</em><strong>"</strong>も行うことにより、行全体をラップする値が切り捨てられることはできません、非常に長い文字列とその文字列に円記号を終了INF ファイルで次の行に連結することはできません。

1 つの国際 INF ファイルを作成する、INF がロケール固有のセットを持つことができます**文字列**。<em>LanguageID</em>セクションで、正式な構文のステートメントのようにします。 *LanguageID*拡張機能は次のように定義されている 16 進数の値。

-   下位 10 ビットは、主言語 ID を含めるし、次の 6 ビットで定義されている MAKELANGID マクロで指定したとおり、サブ言語 ID を含めることが*Winnt.h*します。
-   言語とサブ言語 Id が Win32 LANG_ のシステム定義の値と一致する必要があります*XXX*と SUBLANG_*XXX*で定義された定数*Winnt.h します。*

たとえば、 *LanguageID* 0x0407 の値は、サブ言語 SUBLANG_GERMAN ID (01) とプライマリ言語 LANG_GERMAN ID (07) を表します。

INF ファイルには、1 つだけ含めることができます**文字列**と共に 1 つのセクション**文字列**。<em>LanguageID</em>の各セクション*LanguageID*値。

Windows は、1 つを選択します。**文字列**すべて % を変換するために使用するセクション*strkey*インストール % トークンです。 Windows の選択に応じて、特定のコンピューターの現在のロケールを**文字列**次のようにセクション。

1.  Windows は最初に、*します。LanguageID* INF でコンピューターに割り当てられている現在のロケールに一致する値。 Windows を使用すると完全に一致が見つかった場合**Strings.LanguageID**すべて % を変換する INF セクション*strkey*INF 内で定義されている % トークンです。
2.  それ以外の場合、Windows は [次へ] と一致する、LANG_*XXX* SUBLANG_NEUTRAL、SUBLANG_ としての値を持つ値*XXX*します。 このような一致が見つかった場合は、Windows を使用して INF セクション変換すべて %*strkey*INF 内で定義されている % トークンです。
3.  それ以外の場合、Windows は [次へ] と一致する、LANG_*XXX*値と任意の有効な SUBLANG_*XXX*同じ LANG_ の*XXX*ファミリ。 このような部分的に一致が見つかった場合は、その Strings.LanguageID INF セクションを使用して、すべて % を変換する*strkey*INF 内で定義されている % トークンです。
4.  それ以外の場合、装飾されていない文字列のセクションのすべてに Windows の使用が % を翻訳*strkey*INF 内で定義されている % トークンです。

慣例により、および、国際市場向けの INF ファイルのセットを作成しやすくするため**文字列**セクションは、すべてのシステム INF ファイル内の最後です。 % を使用して*strkey*、INF、およびロケールごとに配置する内のすべてのユーザーに表示される文字列値の % トークン**文字列**セクションで、このような文字列の変換を簡略化します。 ロケールに固有の INF ファイルの詳細については、次を参照してください。 [International INF ファイルの作成](creating-international-inf-files.md)です。

**文字列**セクションは、すべての INF ファイルの最後のセクションで、% を指定した*strkey*% のトークンで定義されている、**文字列**でセクションを繰り返し、他の場所で使用できる、INF、具体的には、場所にそのトークンの変換された値が必要です。 [SetupAPI](setupapi.md)関数展開の各 %*strkey*% トークン、指定した文字列とさらに処理する INF の値を展開し使用します。

% の使用*strkey*INF ファイル内の % トークンはユーザーに表示される文字列値に制限されません。 内の各トークンが定義されていれば、INF ライターに便利な方法でこれらのトークンを使用できる、**文字列**セクション。 たとえば、いくつかの Guid の仕様を必要とする INF ファイルを作成する場合があります % を作成すると便利*strkey*各 GUID 値の代わりにわかりやすい名前を使用して、guid ごと % トークンです。

セットを指定する**%** <em>strkey</em>**% ="{**<em>GUID</em>**}"** INF ファイルの値**文字列**セクションでは、各明示的な GUID 値を 1 回だけ入力する必要があります。 こうと、INF ファイルで明示的な GUID 値を使用して、読みやすくの内部 INF ドキュメントを提供します。

すべての %*strkey*% トークンは、参照されている INF ファイルで定義する必要があります。 持つ任意の INF ファイルのため、 **Include**と**必要がある**エントリ、含まれる、INF する必要がありますが、独自**文字列**すべて % を定義するセクション*strkey*% トークンがその INF で参照されています。

INF で**文字列** セクションで、終端の NULL 文字を含む、置換文字列の文字の最大長は 4096 (Windows Vista および Windows の以降のバージョン) と 512 (Windows Server 2003、Windows XP、およびWindows 2000)。 文字列の置換後は、INF ファイルの文字列の文字の最大長は、4096、終端の NULL 文字を含むです。

<a name="examples"></a>使用例
--------

次の例の一部を示しています、**文字列**システム提供のロケール固有のセクション*dvd.inf*英語圏の国/地域でインストールするためです。

```ini
[Strings]
Msft="Microsoft"
MfgToshiba="Toshiba"
Tosh404.DeviceDesc="Toshiba DVD decoder card"
; ... 
```

次の例では、文字列の連結を示します。

```ini
[OEM Windows System Component Verification]
OID = 1.3.6.1.4.1.311.10.3.7    ; WHQL OEM OID 
Notice = "%A% %B% %C% %D% %E%" 
[Strings]
A = "This certificate is used to sign untested drivers that have not passed the Windows Hardware Quality Labs (WHQL) testing process."
B = "This certificate and drivers signed with this certificate are intended for use in test environments only, and are not intended for use in any other context."
C = "Vendors who distribute this certificate or drivers signed with this certificate outside a test environment may be in violation of their driver signing agreement."
D = "Vendors who have their drivers signed with this certificate do so at their own risk." 
E = "In particular, Microsoft assumes no liability for any damages that may result from the distribution of this certificate or drivers signed with this certificate outside the test environment described in a vendor's driver signing agreement."
```

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[***DDInstall *。サービス**](inf-ddinstall-services-section.md)

[**製造元**](inf-manufacturer-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[***モデル***](inf-models-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**バージョン**](inf-version-section.md)

 

 







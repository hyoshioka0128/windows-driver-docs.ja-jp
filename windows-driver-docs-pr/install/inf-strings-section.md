---
title: INF Strings セクション
description: INF ファイルには、その INF の別の場所で指定されたすべての strkey トークンを定義するために、少なくとも1つの文字列セクションが必要です。
ms.assetid: 7352aa82-a7cd-4d15-9a9e-e03985f6006e
keywords:
- INF 文字列セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Strings Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d7b9c2a137f5cd12ef7f912a450f983b9851c03
ms.sourcegitcommit: 6e2986506940c203a6a834a927a774b7efa6b86e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82800095"
---
# <a name="inf-strings-section"></a>INF Strings セクション


INF ファイルには、その INF の別の場所で指定された%*strkey*% トークンをすべて定義するために、少なくとも1つの**文字列**セクションが必要です。

```inf
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


<a href="" id="strkey1--strkey2-----"></a>*strkey1*、 *strkey2*、...  
INF ファイル内の各文字列キーは、文字、数字、およびその他の明示的に表示されている文字で構成される一意の名前を指定する必要があります。 このような*strkey*トークン内の% 文字は、と**%%** して表す必要があります。

<a href="" id="some-string----some-string-"></a>*文字列* | **"**<em>some string</em>**"**  
文字列を指定します。必要に応じて、文字、数字、句読点、および場合によっては、特定の暗黙的に表示される文字 (特定の内部スペースやタブ文字を含む) を含む、二重引用符文字 (") を使用して区切ります。 ただし、引用符で囲まれていない文字列には、内部の二重引用符 (")、セミコロン (;)、改行、リターン、または非表示のコントロール文字を\)含めることはできません。また、末尾の文字として円記号を使用することはできません。

<a href="" id="------string-with-leading-or-trailing-whitespace-----------"></a>**"* **     文字列-先頭または末尾の空白文字*     **" * * |   

<a href="" id="-very-long-multiline-string----"></a>**"**<em>非常に長い-複数行文字列</em>**"** |   

<a href="" id="-string-with-semicolon----"></a>**"**<em>文字列-セミコロン</em>**"** |   

<a href="" id="-string-ending-in-backslash---"></a>**"**<em>文字列の末尾に円記号</em>を指定する **"** |  

<a href="" id="--double-quoted-string-value--"></a>**"***" 二重引用符で囲まれた文字列-値 "***"**  
%*Strkey*% トークンに対して指定された値は、次のいずれかの条件を満たしている場合は、二重引用符 (") で囲む*必要があり*ます。

-   指定した文字列の先頭または末尾に空白が含まれていて、その値の一部として保持する必要がある場合、その文字列を二重引用符で囲む必要があります。これにより、その文字列の先頭または末尾の空白文字が INF パーサーによって破棄されるのを防ぐことができます。
-   長い文字列に、テキストエディターでの行の折り返しによって内部の改行文字または復帰文字を含めることができる場合は、最初の内部ラインフィードまたは復帰文字で文字列が切り捨てられないように、二重引用符で囲む必要もあります。
-   このような文字列にセミコロンが含まれている場合は、文字列がセミコロンで切り捨てられないように、二重引用符で囲む必要があります。 ( [Inf ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)に記載されているように、セミコロン文字は inf ファイルの各コメントを開始します)。
-   このような文字列が円記号で終わっている場合は、文字列が次のエントリと連結されないように、二重引用符で囲む必要があります。 (INF ファイルの一般的な構文規則に記載されているように\) 、円記号 () は、inf ファイルの行の繰り返しとして使用されます。
-   引用符で囲まれていない文字列の指定と同様に、"引用符で囲まれた文字列" には、内部の二重引用符文字を含めることはできません。 ただし、二重引用符文字の1つ以上の組み合わせを使用して、明示的に二重引用符で囲まれた文字列値として指定することができます (たとえば、"" 一部の文字列 "")。

    INF パーサーは、このセクションの "引用符で囲まれた文字列" に対して最も外側にある二重引用符のペアを破棄するだけでなく、後続の2つの連続する二重引用符のペアを1つの二重引用符文字にでは、ます。

    たとえば、"" "などの文字列" "" は、解析時に "some string" にもなります。

まとめると、次のいずれかに該当する場合は、任意の文字列を二重引用符文字 (") のペアで囲む必要があります。

-   文字列には、先頭または末尾の空白文字が含まれます。
-   文字列は、行が折り返される長さです。
-   この文字列には、セミコロンまたは最後の円記号が含まれています。
-   文字列自体は引用符で囲まれた文字列です。

システム INF パーサーは、このような文字列を区切る最も外側の二重引用符文字と、二重引用符で囲まれた文字列の区切り記号の外側にある先頭または末尾の空白文字を破棄します。

<a name="remarks"></a>解説
-------

システム inf パーサーは、%*strkey*% トークンを定義する任意の **"**<em>引用符で囲ま</em>れた文字列 **"** から外側の二重引用符のうち最も外側のペアを取り除きます。そのため、多くのシステム inf ファイルでは、すべての%*strkey*% トークンが **"**<em>引用符で囲ま</em>れた文字列<strong>"</strong>として定義されています。 また、 **"**<em>引用符で囲ま</em>れた文字列<strong>"</strong>を使用すると、行を囲む長い文字列値を切り捨てられず、末尾の円記号を含む文字列を INF ファイルの次の行に連結できなくなります。

1つの国際 INF ファイルを作成するには、一連のロケール固有の文字列を INF に含めることができ**ます。**<em>LanguageID</em>セクションを参照してください。 *LanguageID*拡張は、次のように定義される16進数の値です。

-   下位10ビットには主言語 ID が含まれ、次の6ビットには、 *winnt.h*で定義されている MAKELANGID マクロで指定されているサブ言語 id が含まれます。
-   言語およびサブ言語 Id は、Winnt に定義されている Win32 LANG_*xxx*および SUBLANG_*xxx*定数のシステム定義値と一致している必要があり*ます。*

たとえば、 *LanguageID*値0x0407 は、サブ言語 id が SUBLANG_GERMAN (01) の LANG_GERMAN (07) の主言語 ID を表します。

INF ファイルには、**文字列**セクションを1つだけ含めることができ**ます。** 各*LanguageID*値の<em>LanguageID</em>セクション。

Windows は、インストールのすべての%*strkey*% トークンを変換するために使用される単一の**文字列**セクションを選択します。 Windows は、特定のコンピューターの現在のロケールに応じて、次の方法で**文字列**セクションを選択します。

1.  Windows では、まず、を検索*します。* コンピューターに割り当てられている現在のロケールに一致する INF の値を LanguageID します。 完全に一致するものが見つかった場合、Windows はその**LanguageID** inf セクションを使用して、inf 内で定義されているすべての%*strkey*% トークンを翻訳します。

    すべての文字列トークンをすべての文字列で複製する必要があり**ます。**<i>*</i>**]** セクション、ローカライズする必要がない数値/固定定数もあります。

2.  それ以外の場合、Windows は、SUBLANG_*xxx*として SUBLANG_NEUTRAL の値を使用して LANG_*XXX*値に一致することを確認します。 このような一致が見つかった場合、Windows はその INF セクションを使用して、INF 内で定義されているすべての%*strkey*% トークンを翻訳します。
3.  それ以外の場合、Windows は次に、同じ LANG_*xxx*ファミリの LANG_*xxx*値と有効な SUBLANG_*xxx*に一致するものを探します。 このような部分的な一致が見つかった場合は、LanguageID INF セクションを使用して、INF 内で定義されているすべての%*strkey*% トークンを翻訳します。
4.  それ以外の場合、Windows は、非装飾文字列セクションを使用して、INF 内で定義されているすべての%*strkey*% トークンを変換します。

慣例により、国際市場向けの一連の INF ファイルを作成しやすくするために、**文字列**セクションはすべてのシステム INF ファイル内で最後にあります。 INF 内のすべてのユーザーに表示される文字列値に%*strkey*% トークンを使用して、それらをロケールごとの**文字列**セクションに配置すると、このような文字列の翻訳が簡略化されます。 ロケール固有の INF ファイルの詳細については、「[国際対応の Inf ファイルの作成](creating-international-inf-files.md)」を参照してください。

**文字列**セクションはすべての inf ファイルの最後のセクションですが、**文字列**セクションで定義されている指定された%*strkey*% token は、特に、そのトークンの翻訳された値が必要な場所であれば、inf 内の他の場所で繰り返し使用できます。 [Setupapi.log](setupapi.md)関数は、各%*strkey*% トークンを指定された文字列に展開し、その展開された値を使用してさらに INF を処理します。

INF ファイル内の%*strkey*% トークンの使用は、ユーザーが参照できる文字列値に制限されていません。 これらのトークンは、各トークンが**文字列**セクション内で定義されていれば、任意の方法で INF ライターに使用できます。 たとえば、いくつかの guid の指定を必要とする INF ファイルを記述する場合、各 guid 値の代替としてわかりやすい名前を使用して、GUID ごとに%*strkey*% トークンを作成すると便利な場合があります。

INF ファイルの**%****文字列**セクションで<em>strkey</em>**% = "{**<em>GUID</em>**}"** の値のセットを指定する場合は、明示的な GUID 値を1回だけ入力する必要があります。 これは、INF ファイル全体で明示的な GUID 値を使用するよりも読みやすい内部 INF ドキュメントを提供するのに役立ちます。

すべての%*strkey*% トークンは、それらが参照されている INF ファイル内で定義されている必要があります。 そのため、**インクルード**され、エントリが**必要**なすべての inf ファイルに対して、含まれる inf には、その inf で参照されるすべての%*strkey*% トークンを定義するための独自の**文字列**セクションが必要です。

INF**文字列**セクションでは、置換文字列の最大文字数 (終端の NULL 文字を含む) は、4096 (windows Vista 以降のバージョンの windows) と 512 (windows Server 2003、windows XP、および windows 2000) です。 文字列の置換後、INF ファイル文字列の最大文字数は、終端の NULL 文字を含む、4096になります。

<a name="examples"></a>例
--------

次の例では、英語圏の国/地域でのインストール用に、システムによって提供されるロケール固有の*dvd-rom*の**文字列**セクションのフラグメントを示します。

```inf
[Strings]
Msft="Microsoft"
MfgToshiba="Toshiba"
Tosh404.DeviceDesc="Toshiba DVD decoder card"
; ... 
```

次の例は、文字列の連結を示しています。

```inf
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

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[***DDInstall *。サーヴィス**](inf-ddinstall-services-section.md)

[**Manufacturer**](inf-manufacturer-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[***モデル***](inf-models-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**Version**](inf-version-section.md)

 

 







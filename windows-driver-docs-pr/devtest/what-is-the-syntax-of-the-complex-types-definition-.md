---
title: 複合型定義の構文
description: 複合型定義の構文
ms.assetid: c378839a-3714-4b4e-94a6-d3e1dcf8a610
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0aacf82901088d30041bb6733e4e5f57d81ac86d
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769610"
---
# <a name="what-is-the-syntax-of-the-complex-types-definition"></a>複合型定義の構文


Windows イベントトレーシング (ETW) は、トレース関数で使用するためのいくつかの単純型と複合型を定義します。 これらの型は、Defaultwpp .ini ファイルで宣言されています。 ただし、独自のカスタム構成ファイルを作成し、それを使用するようにすることもできます。

複合データ型の定義 \_ cplx 型の形式 \_ は次のとおりです。

```
DEFINE_CPLX_TYPE(TypeName, HelperMacroName, ArgumentType, WppMofType,"WppMofFormat", TypeSignature, Priority, Slots);
```

次に例を示します。

```
DEFINE_CPLX_TYPE(.*ls, WPP_LOGXWCS, const xwcs_t&, ItemPWString,"s", _xwcs_t_, 0, 2);
```

### <a name="span-idformat_elementsspanspan-idformat_elementsspanformat-elements"></a><span id="format_elements"></span><span id="FORMAT_ELEMENTS"></span>要素の書式設定

<span id="TypeName"></span><span id="typename"></span><span id="TYPENAME"></span>*TypeName*  
WPP は、このフィールドを使用して複合型を識別します。 たとえば、のように**なります。 \*ls**。

<span id="HelperMacroName"></span><span id="helpermacroname"></span><span id="HELPERMACRONAME"></span>*//マクロ*  
長さとアドレスのペアの形式で引数を可変長配列に変換するヘルパーマクロ。 この形式は、変数引数リストの各エントリに対して、 **TraceMessage**関数によって必要になります。

引数を適切に書式設定するには、次の例に示すように、ヘルパーマクロの定義で[**WPP \_ logpair**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556197(v=vs.85))マクロを使用する必要があります。

```
#define HelperMacroName(x) WPP_LOGPAIR(length, x)
```

**メモ**   実装するトレースロジックによっては、複数の WPP logpair マクロを使用してマクロを定義することが必要になる場合があり \_ ます。

 

<span id="Argument_Type"></span><span id="argument_type"></span><span id="ARGUMENT_TYPE"></span>*引数の型*  
*TypeName*型の引数が受け入れることができる値を示します。 たとえば、 **const xwcs \_ t&** です。

<span id="WppMofType"></span><span id="wppmoftype"></span><span id="WPPMOFTYPE"></span>*WppMofType*  
WPP プリプロセッサによって認識される管理オブジェクトフォーマット (MOF) の種類を指定します。

<span id="WppMofFormat"></span><span id="wppmofformat"></span><span id="WPPMOFFORMAT"></span>*WppMofFormat*  
WPP プリプロセッサによって認識される **"s"** などの書式指定子を指定します。

<span id="TypeSignature"></span><span id="typesignature"></span><span id="TYPESIGNATURE"></span>*TypeSignature*  
複合型に関連付けられるように、関数名に付加される文字列。 アンダースコアの間には1文字または複数の文字が必要です。 たとえば、「 ** \_ xwcs \_ t \_ **」とします。

<span id="Priority"></span><span id="priority"></span><span id="PRIORITY"></span>*的*  
この要素は予約されており、0に設定する必要があります。

<span id="Slots"></span><span id="slots"></span><span id="SLOTS"></span>*スロット*  
WPP プリプロセッサがこの複合型の[TraceMessage](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-tracemessage)関数に渡す可変長パラメーターの最大数を指定します。 この format 要素は省略可能です。 この要素が指定されていない場合、WPP は既定値の1を使用します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

複合型を定義するには、次の手順を実行します。

1.  ローカル構成ファイルを作成します。 このファイルには、 \_ \_ 複合型を定義する cplx 型マクロの定義が含まれている必要があります。

2.  ローカル構成ファイルを[WPP プリプロセッサ](wpp-preprocessor.md)に指定します。 プロジェクトのプロパティを開きます。 [ **WPP トレース**] の [**ファイルオプション**] で、[**追加の構成ファイル**] フィールドを使用して構成ファイルの名前を指定します (**-ini**パラメーター)。 Wpp のトレースを有効にするには、[**実行する Wpp** **] を [はい]** に設定します。 詳細については、「WPP プリプロセッサ」を参照してください。

たとえば、という名前の複合型を定義するローカル構成ファイル (Localwpp .ini) を作成でき**ます。 \*ls**。 複合型は、次のように定義します。

```
DEFINE_CPLX_TYPE(.*ls, WPP_LOGXWCS, const xwcs_t&, ItemPWString,"s", _xwcs_t_, 0, 2);
```

次に、WPP が型を確認し**ます。 \*ls**(など):

```
printf("my string is %.*ls", value);
```

WPP は次のステージング関数を生成します ( **SF**は "ステージング関数" を表します)。

```
WPP_SF__xwcs_t_(..., const xwcs_t& a1) {
    TraceMessage(..., WPP_LOGXWCS(a1) 0);
}
```

次に、WPP は、次の文字列のような MOF エントリを生成し**ます。 \*ls**型名は、適切な MOF 形式 **% s**に置き換えられます。

```
"my string is %s"
{
    Value, ItemPWString
}
```

また、型の構造も生成します。たとえば、

```
struct xwcs_t {
      WCHAR*    _buf;
      short     _len;
      xwcs_t(short buf, short len):_buf(buf),_len(len){}
};
```

ここで、次のように、データ型を**xwstr \_ t**型の文字列に結合するマクロを追加します。

```
#define WPP_LOGXWCS(x) WPP_LOGPAIR(2, &(x)._len) WPP_LOGPAIR((x)._len, (x)._buf)
```

ここで、 **Itempwstring**は、WPP によって認識される、カウントされた Unicode 文字列型です。 長さは2バイトとして指定されます。

ETW は、WPP logxwcs 定義を解釈するときに \_ 、最初の[**wpp \_ logpair**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556197(v=vs.85))マクロが解釈されるバッファーに2バイトの文字列を格納します。 Etw は、ETW が2番目の WPP \_ logpair マクロを解釈するときに、文字列のすべてのバイトをバッファーにコピーします。

長さはデータとは別に指定したので、WPP \_ logxwcs は[TraceMessage](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-tracemessage)の2つのスロットを使用します。 したがって、数値**2**は8番目の引数です。

[WPP プリプロセッサ](wpp-preprocessor.md)を呼び出すときは、[**感嘆符を無視**する] オプション (**-noshrieks**) を使用します。 これにより、WPP は、感嘆符 (!) で囲まれていない名前を持つ複合型を認識できます ("shrieks" とも呼ばれます)。

WPP トレースオプションの完全な一覧と、プロジェクトプロパティページからの設定方法については、「 [Wpp プリプロセッサ](wpp-preprocessor.md)」を参照してください。

 

 






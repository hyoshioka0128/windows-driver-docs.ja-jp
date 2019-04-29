---
title: 複合型定義の構文とは
description: 複合型定義の構文とは
ms.assetid: c378839a-3714-4b4e-94a6-d3e1dcf8a610
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68dc7cce9f5340b4f4a7a47c9c7a7cdea228b681
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386361"
---
# <a name="what-is-the-syntax-of-the-complex-types-definition"></a>複合型定義の構文


Event Tracing for Windows (ETW) トレース関数で使用するためのいくつかの単純および複雑な型を定義します。 これらの型は、Defaultwpp.ini ファイルで宣言されます。 ただし、独自のカスタム構成ファイルを作成し、それを使用する WPP をダイレクトすることができます。

複雑なデータ型の定義の形式\_CPLX\_型では、次に示します。

```
DEFINE_CPLX_TYPE(TypeName, HelperMacroName, ArgumentType, WppMofType,"WppMofFormat", TypeSignature, Priority, Slots);
```

次に、例を示します。

```
DEFINE_CPLX_TYPE(.*ls, WPP_LOGXWCS, const xwcs_t&, ItemPWString,"s", _xwcs_t_, 0, 2);
```

### <a name="span-idformatelementsspanspan-idformatelementsspanformat-elements"></a><span id="format_elements"></span><span id="FORMAT_ELEMENTS"></span>要素の書式設定

<span id="TypeName"></span><span id="typename"></span><span id="TYPENAME"></span>*TypeName*  
WPP は、複合型を識別するために、このフィールドを使用します。 たとえば、 **.\*%.*ls**します。

<span id="HelperMacroName"></span><span id="helpermacroname"></span><span id="HELPERMACRONAME"></span>*HelperMacroName*  
長さ/アドレスのペアの形式で可変長配列を引数に変換するヘルパー マクロ。 この形式が必要、 **TraceMessage**の可変個引数リスト内のエントリの各関数。

引数を正しく書式設定を使用する必要があります、 [ **WPP\_LOGPAIR** ](https://msdn.microsoft.com/library/windows/hardware/ff556197)マクロでは、次の例に示すように、ヘルパー マクロの定義。

```
#define HelperMacroName(x) WPP_LOGPAIR(length, x)
```

**注**  が実装するトレース ロジックによっては、複数の WPP を使用して、マクロを定義する必要があります\_LOGPAIR マクロ。

 

<span id="Argument_Type"></span><span id="argument_type"></span><span id="ARGUMENT_TYPE"></span>*引数の型*  
その引数の値を示します*TypeName*型を受け入れることができます。 たとえば、 **const xwcs\_t &** します。

<span id="WppMofType"></span><span id="wppmoftype"></span><span id="WPPMOFTYPE"></span>*WppMofType*  
WPP プリプロセッサによって認識される管理オブジェクト フォーマット (MOF) の種類を指定します

<span id="WppMofFormat"></span><span id="wppmofformat"></span><span id="WPPMOFFORMAT"></span>*WppMofFormat*  
など、書式指定子を指定 **"s"**、つまり、WPP プリプロセッサによって認識されます。

<span id="TypeSignature"></span><span id="typesignature"></span><span id="TYPESIGNATURE"></span>*TypeSignature*  
複合型との関連付けの関数名に追加された文字列。 1 つの文字またはアンダー スコアとの間の複数の文字の必要があります。 たとえば、  **\_xwcs\_t\_** します。

<span id="Priority"></span><span id="priority"></span><span id="PRIORITY"></span>*優先順位*  
この要素は、予約されており、0 に設定する必要があります。

<span id="Slots"></span><span id="slots"></span><span id="SLOTS"></span>*スロット*  
WPP プリプロセッサに渡すパラメーターを可変長の最大数を指定します、 [TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)この複合型の関数。 この形式の要素は省略可能です。 この要素が指定されていない場合、WPP は既定値の 1 を使用します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

複合型を定義するには、次の操作を行います。

1.  ローカル構成ファイルを作成します。 このファイルには、定義が含まれている必要があります\_CPLX\_複合型を定義するマクロ。

2.  ローカル構成ファイルを指定、 [WPP プリプロセッサ](wpp-preprocessor.md)します。 プロジェクトのプロパティを開きます。 **WPP トレース**、**ファイル オプション**を使用して、**追加の構成ファイル**構成ファイルの名前を指定するフィールド (**ini**パラメーター)。 設定によって、WPP トレースを有効にすることを確認する**実行 WPP**に**はい**します。 詳細については、WPP プリプロセッサを参照してください。

たとえば、という名前の複合型を定義するローカル構成ファイル (Localwpp.ini) を作成できます **.\*%.*ls**します。 次のように、複合型を定義します。

```
DEFINE_CPLX_TYPE(.*ls, WPP_LOGXWCS, const xwcs_t&, ItemPWString,"s", _xwcs_t_, 0, 2);
```

型を認識すると次に、WPP **.\*%.*ls**などで。

```
printf("my string is %.*ls", value);
```

WPP には、次のステージング関数が生成されます (ここ**SF** "関数を staging"を表します)。

```
WPP_SF__xwcs_t_(..., const xwcs_t& a1) {
    TraceMessage(..., WPP_LOGXWCS(a1) 0);
}
```

WPP、MOF エントリは、次の文字列などを生成し、場所、 **.\*%.*ls**型名は、適切な MOF の形式に置き換えられます **%s**します。

```
"my string is %s"
{
    Value, ItemPWString
}
```

これもなどが生成される型、構造体

```
struct xwcs_t {
      WCHAR*    _buf;
      short     _len;
      xwcs_t(short buf, short len):_buf(buf),_len(len){}
};
```

これで、データ型を型の文字列に結合するマクロを追加**xwstr\_t**、次のようにします。

```
#define WPP_LOGXWCS(x) WPP_LOGPAIR(2, &(x)._len) WPP_LOGPAIR((x)._len, (x)._buf)
```

場所**ItemPWString** WPP によって認識されるカウント対象の Unicode 文字列型です。 長さは、2 バイトとして指定されます。

ETW が、WPP はどのように解釈するときに\_LOGXWCS 定義では、2 バイト文字列を最初のバッファーに入れ[ **WPP\_LOGPAIR** ](https://msdn.microsoft.com/library/windows/hardware/ff556197)マクロが解釈されます。 ETW し、文字列のすべてのバイトのバッファーにコピー ETW 2 つ目の WPP を解釈するときに\_LOGPAIR マクロ

データ、WPP とは別の長さを指定したため、\_LOGXWCS の 2 つのスロットを消費する[TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)します。 そのため、数**2**は 8 番目の引数です。

呼び出すときに、 [WPP プリプロセッサ](wpp-preprocessor.md)を使用して、**無視の感嘆符**オプション (**- noshrieks**)。 これにより、WPP「途切れ」とも呼ばれますの感嘆符 (!) で囲まれていない名前を持つ複合型を認識するには

プロジェクトのプロパティ ページで設定する方法については、WPP トレース オプションの完全な一覧を参照してください。 [WPP プリプロセッサ](wpp-preprocessor.md)します。

 

 






---
title: ブレークポイントの構文
description: このトピックでは、ブレークポイントの構文をについて説明します
ms.assetid: 86228b87-9ca3-4d0c-be9e-63446ac6ce31
keywords: デバッガー, ブレークポイントは、メソッド、ブレークポイント、コマンド、b (ブレークポイント識別子)、リテラルの MASM 識別子、template 宣言された関数の構文規則
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b714acd984506f36205285f0c61cd90e43c839b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347859"
---
# <a name="breakpoint-syntax"></a>ブレークポイントの構文


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


作成時に、次の構文要素を使用できる、[ブレークポイント](using-breakpoints.md)、デバッガー コマンド ウィンドウまたは WinDbg のグラフィカル インターフェイスを使用します。

### <a name="span-idaddressesinbreakpointsspanspan-idaddressesinbreakpointsspanaddresses-in-breakpoints"></a><span id="addresses_in_breakpoints"></span><span id="ADDRESSES_IN_BREAKPOINTS"></span>ブレークポイントのアドレス

ブレークポイントは、さまざまな種類の仮想アドレス、関数のオフセット、およびソース行番号を含む、アドレス構文のサポートします。 たとえば、ブレークポイントを設定するのに次のコマンドを使用できます。

```dbgcmd
0:000> bp 0040108c
0:000> bp main+5c
0:000> bp `source.c:31`
```

この構文の詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)、[ソース行構文](source-line-syntax.md)、および個々 のコマンドのトピックです。

### <a name="span-idbreakpointsonmethodsspanspan-idbreakpointsonmethodsspanbreakpoints-on-methods"></a><span id="breakpoints_on_methods"></span><span id="BREAKPOINTS_ON_METHODS"></span>メソッドのブレークポイント

ブレークポイントを設定する場合、 *MyMethod*メソッドで、 *MyClass*クラス、2 つの異なる構文を使用することができます。

-   MASM の式の構文では、2 つのコロンをするか、二重アンダー スコアをメソッドを指定できます。

    ```dbgcmd
    0:000> bp MyClass::MyMethod 
    0:000> bp MyClass__MyMethod 
    ```

-   C++ 式の構文では、二重のコロンでメソッドを示す必要があります。

    ```dbgcmd
    0:000> bp @@( MyClass::MyMethod ) 
    ```

複雑なブレークポイント コマンドを使用する場合は、MASM 式の構文を使用する必要があります。 式の構文の詳細については、次を参照してください。[を評価する式](evaluating-expressions.md)します。

### <a name="span-idbreakpointsusingcomplicatedtextspanspan-idbreakpointsusingcomplicatedtextspanbreakpoints-using-complicated-text"></a><span id="breakpoints_using_complicated_text"></span><span id="BREAKPOINTS_USING_COMPLICATED_TEXT"></span>複雑な文字を使用してブレークポイント

C++ のパブリック クラスのメンバーと同様に、スペースを含めることがある関数などの複雑な関数にブレークポイントを設定するには、かっこで囲まれた式を囲みます。 たとえば、使用して**bp (?MyPublic)** または**bp (新しい演算子)** します。

汎用的な手法を使用して、@!"文字"構文。 これは、特別なエスケープ MASM エバリュエーター シンボル解決の任意のテキストを提供することができるのです。 3 つの記号で開始する必要があります @!" 引用符 (") で終わります。 この構文を使用しないで、スペース、山かっこを使用することはできません (&lt;、 &gt;)、またはシンボル名 MASM エバリュエーターに他の特殊文字。 この構文では、専用の名前、およびパラメーターではありません。 テンプレートとオーバー ロードは、この見積もり表記を必要とするシンボルの主要なソースをします。 設定することも、 **bu**コマンドを使用して、@!"文字の"構文を次のコード例に示すよう。

```dbgcmd
0:000> bu @!"ExecutableName!std::pair<unsigned int,std::basic_string<unsigned short,std::char_traits<unsigned short>,std::allocator<unsigned short> > >::operator="
```

この例で*ExecutableName*実行可能ファイルの名前を指定します。

このエスケープ構文が C 関数の名前にあるスペース (または特殊文字) にはないため、有用な C ではなく C++ (たとえば、オーバー ロードされた演算子)。 ただし、この構文は、.NET Framework でオーバー ロードのかなり使用しているため、多くのマネージ コードの重要なもなりました。

C++ 構文で任意のテキストにブレークポイントを設定するには使用<strong>@ bu@c+ (</strong><em>テキスト</em> **)** C++ と互換性のあるシンボル。

### <a name="span-idbreakpointsinscriptsspanspan-idbreakpointsinscriptsspanbreakpoints-in-scripts"></a><span id="breakpoints_in_scripts"></span><span id="BREAKPOINTS_IN_SCRIPTS"></span>スクリプト内のブレークポイント

ブレークポイント Id は、明示的に参照する必要はありません。 ブレークポイントの ID に対応する整数値に解決される数値式を使用する代わりに、 でのブレークポイントとして式を解釈することを示すには、次の構文を使用します。

```dbgcmd
b?[Expression]
```

この構文で、角かっこが必要なおよび*式*ブレークポイント ID に対応する整数値に解決される任意の数値式の略

この構文ではデバッガーのスクリプトをプログラムでブレークポイントを選択します。 次の例では、ブレークポイントは、ユーザー定義の擬似レジスタの値に応じて変更します。

```dbgcmd
b?[@$t0]
```

### <a name="span-idbreakpointpseudoregistersspanspan-idbreakpointpseudoregistersspanbreakpoint-pseudo-registers"></a><span id="breakpoint_pseudo_registers"></span><span id="BREAKPOINT_PSEUDO_REGISTERS"></span>ブレークポイントの擬似レジスタ

式の中でブレークポイントのアドレスを参照する場合は、使用、[擬似レジスタ](pseudo-register-syntax.md)で、* *$bp * * * 数*構文、場所*数*はブレークポイントの ID です。 この構文の詳細については、擬似レジスタの構文を参照してください。

 

 






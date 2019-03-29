---
title: 作成する方法カスタム WPP 拡張書式指定文字列
description: 作成する方法カスタム WPP 拡張書式指定文字列
ms.assetid: 6c4c47c6-71b2-48a0-bab3-8498029b8244
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc4778aab27945662eca2422ae55cb594c516632
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464266"
---
# <a name="how-do-i-create-custom-wpp-extended-format-specification-strings"></a>カスタムの WPP 拡張書式指定文字列を作成する方法


定義を使用してカスタム WPP 拡張形式仕様の文字列を作成する\_CPLX\_マクロ。 このマクロを使用する方法の詳細については、次を参照してください。[定義の種類の複雑な構文とは何ですか?](what-is-the-syntax-of-the-complex-types-definition-.md)します。

このトピックでは、以下を行う方法を説明する例を示します。

- [仕様の文字列形式を拡張するカスタム WPP トレース固定長文字列](#trace-fixed-length-strings-through-custom-wpp-extended-format-specification-strings)

- [カスタム拡張 WPP 形式仕様の文字列を使用して可変長文字列をトレースします。](#trace-variable-length-strings-through-custom-wpp-extended-format-specification-strings)

これらの例の各定義の定義のカスタム WPP 構成ファイルの使用を示しています\_CPLX\_マクロ。 これらの例では、構成ファイルを LocalWpp.ini と呼びます。 カスタム WPP 構成ファイルを使用する方法の詳細については、次を参照してください。[カスタム データ型を定義する方法でしょうか。](how-do-you-define-custom-data-types-.md)します。

## <a name="trace-fixed-length-strings-through-custom-wpp-extended-format-specification-strings"></a>仕様の文字列形式を拡張するカスタム WPP トレース固定長文字列

この例では、カスタム WPP を使用して、ネットワーク アドレス拡張書式指定文字列トレース インターネット プロトコル バージョン 6 (IPv6) にする方法を示しています。 IPv6 ネットワーク アドレスを in6 で定義されている\_addr 構造体を 16 バイトの固定長の長さであります。

この例では、複雑なデータ型 (IPV6ADDR) が定義されて、% として使用できます。IPV6ADDR! ソース コード内の指定の文字列をフォーマットします。

IPV6ADDR 複雑なデータ型を作成するには、LocalWpp.ini 構成ファイルに次のステートメントを追加します。

1.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>DEFINE_CPLX_TYPE(IPV6ADDR, WPP_LOGIPV6, in6_addr *, ItemIPV6Addr, "s", _IPV6_, 0, 1);</code></pre></td>
    </tr>
    </tbody>
    </table>

    このステートメントは、定義を使用して\_CPLX\_マクロの引数の型など、その属性と共に、複合型 (IPV6ADDR) を定義する (in6\_addr \*) とサイズ (16)。

    ステートメントでは、ヘルパー マクロの名前も指定します (WPP\_LOGIPV6) のソース コード内の IPV6ADDR 複合型を解析するとき、WPP プリプロセッサによって使用される、[トレース プロバイダー](trace-provider.md)します。

2.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>WPP_FLAGS(-DWPP_LOGIPV6(x) WPP_LOGPAIR( (16), (x)));</code></pre></td>
    </tr>
    </tbody>
    </table>

    このステートメントに渡されると、IPV6 の引数の長さ/アドレスの組み合わせを書式設定に使用されるヘルパー マクロの定義、 [TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)関数。

Visual Studio でプロジェクトのプロパティ ページを開きます。 **WPP トレース**、**ファイル オプション**、LocalWpp.ini としてを指定、**追加の構成ファイル**します。 参照してください[WPP プリプロセッサ](wpp-preprocessor.md)詳細についてはします。

次のサンプル ソース コードに示す方法、[トレース プロバイダー](trace-provider.md) % を使用して、IPv6 ネットワーク アドレスをトレースすることができます。IPV6ADDR! 書式指定文字列:

```
struct in6_addr IPAddressV6 = {0};
DoTraceMessage(Noise, "IN6_ADDR  = %!IPV6ADDR!", &IPAddressV6);
```

**注**  トレース固定長のメディア アクセス制御 (MAC) アドレスの複合型 (MACADDR) を作成することができます。 IPV6ADDDR 複合型を使用した手順を実行して、この複合型を指定できます。

 

## <a name="trace-variable-length-strings-through-custom-wpp-extended-format-specification-strings"></a>カスタム拡張 WPP 形式仕様の文字列を使用して可変長文字列をトレースします。

この例では、書式指定文字列を拡張するカスタム WPP を使用してデータの可変長バッファーをトレースする方法を示します。

この例で、% として、使用できる複合データ型 (16 進ダンプ) が定義されています!16 進ダンプ。 ソース コード内の指定の文字列をフォーマットします。

16 進ダンプの複雑なデータ型を作成するには、LocalWpp.ini 構成ファイルに次のステートメントを追加します。

1.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>DEFINE_CPLX_TYPE(HEXDUMP, WPP_LOGHEXDUMP, const xstr_t&, ItemHEXDump,"s", _HEX_, 0, 2);</code></pre></td>
    </tr>
    </tbody>
    </table>

    このステートメントは、定義を使用して\_CPLX\_マクロの引数の型など、その属性と共に、複合型 (16 進ダンプ) を定義する (const [xstr]\_t &)に渡されるパラメーターの数と**TraceMessage** (2)。 この複合型が可変長データは、マクロの使用されるため、**サイズ**要素が 0 に設定します。

    ステートメントでは、ヘルパー マクロの名前も指定します (WPP\_LOGHEXDUMP) のソース コード内の 16 進ダンプの複合型を解析するとき、WPP プリプロセッサによって使用される、[トレース プロバイダー](trace-provider.md)します。

2.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>struct xstr_t {
       CHAR * _buf;
       short _len;
       xstr_t(__in_ecount(len) char *buf, short len):_buf(buf),_len(len) {}
    };</code></pre></td>
    </tr>
    </tbody>
    </table>

    このステートメントは、長さと可変長バッファーのアドレスを保存するために使用する構造体を定義します。 ログにこの構造体が初期化されて\_LENSTR のマクロの呼び出しごとにローカルと[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)内を使用する 16 進ダンプの複合型、 *FormatString*パラメーター。

3.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>WPP_FLAGS(-DLOG_LENSTR(len,str)=xstr_t(str,len));</code></pre></td>
    </tr>
    </tbody>
    </table>

    このステートメントは、[xstr] を初期化するために使用されるマクロを定義します。\_可変長バッファーの t の構造体。 このマクロを使用して、内の可変長バッファーを渡す必要があります、 *VariableList*パラメーターの[ **DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918)します。

4.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>WPP_FLAGS(-DWPP_LOGHEXDUMP(x) WPP_LOGPAIR(2,&(x)._len) WPP_LOGPAIR((x)._len, (x)._buf));</code></pre></td>
    </tr>
    </tbody>
    </table>

    このステートメントに渡されると、可変長バッファー引数の長さ/アドレスの組み合わせを書式設定に使用されるヘルパー マクロの定義、 [TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)関数。

    可変長の引数には、2 つの長さ/アドレスの組み合わせが必要です。 その結果、WPP\_LOGHEXDUMP マクロは、WPP 2 つの呼び出しを定義します。\_LOGPAIR 次のようにします。

    -   最初の呼び出し WPP\_LOGPAIR は可変長バッファーのサイズを渡します。
    -   WPP の 2 番目の呼び出し\_LOGPAIR 自体のバッファーのアドレスを渡します。

    **注**  このマクロである必要があります、[xstr]\_t 構造がログへの呼び出しで、可変長バッファーの初期化されて\_LENSTR します。 その結果、可変長バッファーを渡す必要があります[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)ログを通じて\_LENSTR マクロ。

     

Visual Studio でプロジェクトのプロパティ ページを開きます。 **WPP トレース**、**ファイル オプション**、LocalWpp.ini としてを指定、**追加の構成ファイル**します。 参照してください[WPP プリプロセッサ](wpp-preprocessor.md)詳細についてはします。

次のサンプル ソース コードに示す方法、[トレース プロバイダー](trace-provider.md) % を使用してデータのバッファーをトレースすることができます。16 進ダンプ。 書式指定文字列:

```
CHAR HexDump[1024] = {0, 1, 2, 3, 4, 5, 6, 7} ;
DoTraceMessage(Noise, "HEXDUMP: %!HEXDUMP! ", LOG_LENSTR(sizeof(HexDump),(PCHAR)HexDump));
```

**注**  可変長バッファーをトレースするため、複合型 (HEXBYTES) を作成することができます。 16 進ダンプの複合型を使用した手順を実行して、この複合型を指定できます。 






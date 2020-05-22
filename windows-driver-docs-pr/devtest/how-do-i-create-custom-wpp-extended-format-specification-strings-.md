---
title: カスタムの WPP 拡張書式指定文字列を作成操作方法には
description: カスタムの WPP 拡張書式指定文字列を作成操作方法には
ms.assetid: 6c4c47c6-71b2-48a0-bab3-8498029b8244
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fb181e34a13f1cd3c4810a70cc0c836f55f9741
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769440"
---
# <a name="how-do-i-create-custom-wpp-extended-format-specification-strings"></a>カスタムの WPP 拡張書式指定文字列を作成する方法


カスタムの WPP 拡張書式指定文字列は、DEFINE \_ cplx 型マクロを使用して作成し \_ ます。 このマクロの使用方法の詳細については、「[複合型の定義の構文](what-is-the-syntax-of-the-complex-types-definition-.md)」を参照してください。

このトピックでは、次の操作方法を示す例について説明します。

- [カスタムの WPP 拡張書式指定文字列を使用して固定長文字列をトレースする](#trace-fixed-length-strings-through-custom-wpp-extended-format-specification-strings)

- [カスタムの WPP 拡張書式指定文字列を使用して可変長文字列をトレースする](#trace-variable-length-strings-through-custom-wpp-extended-format-specification-strings)

これらの各例では、cplx TYPE マクロの定義にカスタムの WPP 構成ファイルを使用する方法を示して \_ \_ います。 これらの例では、構成ファイルの名前は LocalWpp .ini です。 カスタム WPP 構成ファイルの使用方法の詳細については、「[カスタムデータ型を定義する方法](how-do-you-define-custom-data-types-.md)」を参照してください。

## <a name="trace-fixed-length-strings-through-custom-wpp-extended-format-specification-strings"></a>カスタムの WPP 拡張書式指定文字列を使用して固定長文字列をトレースする

この例では、カスタムの WPP 拡張書式指定文字列を使用して、インターネットプロトコルバージョン 6 (IPv6) ネットワークアドレスをトレースする方法を示します。 In6 addr 構造体で定義されている IPv6 ネットワークアドレスには、 \_ 16 バイトの固定長の長さがあります。

この例では、複合データ型 (IPV6ADDR) が定義されています。これは%! として使用できます。IPV6ADDR! ソースコード内の指定文字列を書式設定します。

IPV6ADDR 複合データ型を作成するには、次のステートメントを LocalWpp 構成ファイルに追加します。

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

    このステートメントでは、cplx 型の定義マクロを使用して、 \_ \_ 引数の型 (in6 \_ addr \* ) やサイズ (16) などの属性と共に複合型 (IPV6ADDR) を定義します。

    また、ステートメントでは、 \_ IPV6ADDR 複合型を[トレースプロバイダー](trace-provider.md)のソースコードで解析するときに、wpp プリプロセッサによって使用されるヘルパーマクロ (wpp LOGIPV6) の名前も指定します。

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

    このステートメントは、 [TraceMessage](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-tracemessage)関数に渡されるときに IPV6 引数の長さとアドレスのペアを書式設定するために使用されるヘルパーマクロを定義します。

Visual Studio で、プロジェクトの [プロパティ] ページを開きます。 [ **WPP トレース**] の [**ファイルオプション**] で、**追加の構成ファイル**として「localwpp. ini」と指定します。 詳細については、「 [WPP プリプロセッサ](wpp-preprocessor.md)」を参照してください。

次のサンプルソースコードは、[トレースプロバイダー](trace-provider.md)が%! を使用して IPv6 ネットワークアドレスをトレースする方法を示しています。IPV6ADDR! 書式指定文字列:

```
struct in6_addr IPAddressV6 = {0};
DoTraceMessage(Noise, "IN6_ADDR  = %!IPV6ADDR!", &IPAddressV6);
```

**メモ**   固定長のメディアアクセス制御 (MAC) アドレスをトレースするための複合型 (MACADDR) を作成できます。 この複合型は、IPV6ADDDR 複合型に使用された手順に従って指定できます。

 

## <a name="trace-variable-length-strings-through-custom-wpp-extended-format-specification-strings"></a>カスタムの WPP 拡張書式指定文字列を使用して可変長文字列をトレースする

この例では、カスタムの WPP 拡張書式指定文字列を使用して、データの可変長バッファーをトレースする方法を示します。

この例では、複合データ型 (HEXDUMP) が定義されています。これは、HEXDUMP! ソースコード内の指定文字列を書式設定します。

HEXDUMP 複合データ型を作成するには、次のステートメントを LocalWpp 構成ファイルに追加します。

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

    このステートメントでは、DEFINE \_ cplx TYPE マクロを使用して、 \_ 引数の型 (const xstr \_ t&) や**TraceMessage**に渡されるパラメーターの数 (2) などの属性と共に複合型 (HEXDUMP) を定義します。 この複合型は可変長データに使用されるため、マクロの**サイズ**要素は0に設定されます。

    また、ステートメントでは、 \_ HEXDUMP 複合型を[トレースプロバイダー](trace-provider.md)のソースコードで解析するときに、wpp プリプロセッサによって使用されるヘルパーマクロ (wpp LOGHEXDUMP) の名前も指定します。

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

    このステートメントは、可変長バッファーの長さとアドレスを保存するために使用される構造体を定義します。 この構造体は、LOG LENSTR マクロで初期化され、 \_ HEXDUMP 複合型が*FormatString*パラメーター内で使用される[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))の各呼び出しに対してローカルです。

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

    このステートメントは、可変長バッファーの xstr t 構造体を初期化するために使用されるマクロを定義 \_ します。 このマクロを使用して、可変長バッファーを[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))の変数*リスト*パラメーターに渡す必要があります。

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

    このステートメントは、 [TraceMessage](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-tracemessage)関数に渡されるときに可変長バッファー引数の長さとアドレスのペアを書式設定するために使用されるヘルパーマクロを定義します。

    可変長の引数には、2つの長さとアドレスのペアが必要です。 その結果、WPP \_ LOGHEXDUMP マクロは、次の方法で、wpp logpair への2回の呼び出しを定義し \_ ます。

    -   WPP logpair の最初の呼び出しでは、 \_ 可変長バッファーのサイズが渡されます。
    -   WPP logpair の2回目の呼び出しでは、 \_ バッファー自体のアドレスが渡されます。

    **メモ**   このマクロでは、 \_ LOG LENSTR を呼び出すことによって、可変長バッファーに対して xstr t 構造体が初期化されている必要があり \_ ます。 そのため、LENSTR マクロを使用して、可変長バッファーを[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))に渡す必要があり \_ ます。

     

Visual Studio で、プロジェクトの [プロパティ] ページを開きます。 [ **WPP トレース**] の [**ファイルオプション**] で、**追加の構成ファイル**として「localwpp. ini」と指定します。 詳細については、「 [WPP プリプロセッサ](wpp-preprocessor.md)」を参照してください。

次のサンプルソースコードは、[トレースプロバイダー](trace-provider.md)が%! を使用してデータのバッファーをトレースする方法を示しています。HEXDUMP! 書式指定文字列:

```
CHAR HexDump[1024] = {0, 1, 2, 3, 4, 5, 6, 7} ;
DoTraceMessage(Noise, "HEXDUMP: %!HEXDUMP! ", LOG_LENSTR(sizeof(HexDump),(PCHAR)HexDump));
```

**メモ**   可変長バッファーのトレース用に複合型 (HEXBYTES) を作成できます。 この複合型は、HEXDUMP 複合型に使用された手順に従って指定できます。 






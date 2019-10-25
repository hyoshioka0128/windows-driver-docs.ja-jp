---
title: 安全な文字列関数の使用
description: 安全な文字列関数の使用
ms.assetid: a84008e8-e490-4640-a734-ef55cfbdfea3
keywords:
- 安全な文字列関数 WDK
- 文字列操作関数 WDK
- WDK の安全な文字列関数をバッファーします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50385b79a16f16d629f05979a1ef618bd845624d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838337"
---
# <a name="using-safe-string-functions"></a>安全な文字列関数の使用





システムのセキュリティに関する多くの問題は、バッファー処理の低下や、バッファーオーバーランが原因で発生します。 多くの場合、不適切なバッファー処理は文字列操作操作に関連付けられます。 CC++ /言語ランタイムライブラリ (**strcat**、 **strcpy**、 **sprintf**など) によって提供される標準の文字列操作関数では、バッファーの末尾を超えて書き込むことはできません。

*安全な文字列関数*と呼ばれる文字列操作関数の2つの新しいセットによって、コード内で適切なバッファー処理を行うための追加処理が提供されます。 これらの安全な文字列関数は、Windows Driver Kit (WDK)、および Microsoft Windows XP SP1 以降のバージョンの Driver Development Kit (DDK) および Windows SDK で使用できます。 これらは、Windows によって提供される組み込みC++の C/対応ルーチンと同様のルーチンを置き換えることを目的としています。

安全な文字列関数の1つのセットは、カーネルモードコードで使用します。 これらの関数は、、Ntstrsafe.h という名前のヘッダーファイルでプロトタイプが指定されています。 このヘッダーファイルと関連付けられているライブラリは、WDK で使用できます。

セーフ文字列関数のもう1つのセットは、ユーザーモードアプリケーションで使用します。 対応するヘッダーファイル Strsafe には、これらの関数のプロトタイプが含まれています。 このファイルと関連付けられているライブラリは、Windows SDK で使用できます。 Strsafe の詳細については、「 [Strsafe 関数の使用](https://go.microsoft.com/fwlink/p/?linkid=165522)」を参照してください。

カーネルモードセーフ文字列関数のセットは、次の2つのサブセットで構成されています。

-   [Unicode および ANSI 文字用の安全な文字列関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

    これらの各関数は、2バイトの Unicode 文字をサポートし、1バイトの ANSI 文字をサポートする A とサフィックスが付いたバージョンで使用できます。 たとえば、2つの文字列を連結し、追加した文字列の長さを制限する[**Rtlstringcbcatn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatna)は、 **Rtlstringcbcatn**および**rtlstringcbna**として使用できます。

-   [UNICODE\_文字列構造の安全な文字列関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

    これらの各関数は、入力パラメーターまたは出力パラメーターとして、またはその両方として[**UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)構造体を受け取ります。 たとえば、 [**RtlStringCbCopyUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestring)は、入力パラメーターとして構造体を受け取り、 [**RtlUnicodeStringCopyString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystring)はその構造を出力パラメーターとして受け取り、 [**RtlUnicodeStringCopy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopy)は両方の構造体を入力として受け入れます。出力パラメーターを指定します。

カーネルモードセーフ文字列関数には、次の機能が用意されています。

-   各セーフ文字列関数は、入力としてコピー先バッファーのサイズを受け取ります。 この関数を使用すると、バッファーの末尾を越えて書き込みが行われないようにすることができます。

-   Unicode および ANSI 文字列関数は、操作によって意図した結果が切り捨てられる場合でも、すべての出力文字列を NULL 文字で終了します。

-   すべてのセーフ文字列関数は、1つの有効な成功コード (STATUS\_SUCCESS) のみを使用して、NTSTATUS 値を返します。

-   ほとんどの安全な文字列関数は、バイトカウントと文字カウントバージョンの両方で使用できます。 たとえば、 [**Rtlstringcbcat で**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcata)は、2つのバイトカウント文字列を連結し、 [**Rtlstringcbcat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcata)で2つの文字カウント文字列を連結しています。

-   ほとんどの安全な文字列関数は、追加機能を提供する、サフィックスの付いた拡張されたバージョンで使用できます。 たとえば、 [**Rtlstringcbcatex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatexa)では、 [**Rtlstringcbcatex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcata)の機能が拡張されています。

ここでは、次のトピックについて説明します。

[カーネルモードセーフ文字列関数の概要](summary-of-kernel-mode-safe-string-functions.md)

[カーネルモードの安全な文字列関数のインポート](importing-kernel-mode-safe-string-functions.md)

 

 





---
title: セーフ文字列関数の使用
description: セーフ文字列関数の使用
ms.assetid: a84008e8-e490-4640-a734-ef55cfbdfea3
keywords:
- WDK の安全な文字列関数
- WDK の文字列操作関数
- バッファー WDK 安全な文字列関数
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee63e77c0760c1aef2619c25e18d0038da4082b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579666"
---
# <a name="using-safe-string-functions"></a>セーフ文字列関数の使用





多くのシステム セキュリティの問題が原因が低いバッファー処理し、結果として得られるバッファー オーバーランです。 不適切なバッファーの処理は、文字列操作の操作に関連付けられては多くの場合です。 C/C++ 言語のランタイム ライブラリによって提供される標準的な文字列操作関数 (**strcat**、 **strcpy**、 **sprintf**など) の書き込みができない操作を行いますバッファーの末尾にあります。

呼び出された文字列操作関数の 2 つの新しいセット*安全な文字列関数*、適切なバッファーが、コード内の処理の追加の処理を提供します。 これらの安全な文字列関数とは、ドライバー開発キット (DDK) と Windows SDK の使用できるは、Windows Driver Kit (WDK) で、Microsoft Windows XP sp1 以降のバージョンです。 組み込みの C と C++ の対応する、Windows によって提供されるようなルーチンを置換することは想定されています。

安全な文字列関数の 1 つのセットはカーネル モード コードで使用されます。 これらの関数は、Ntstrsafe.h をという名前のヘッダー ファイルはプロトタイプ宣言します。 このヘッダー ファイルと、関連するライブラリは、WDK で利用します。

その他の一連の安全な文字列関数はユーザー モード アプリケーションで使用されます。 対応するヘッダー ファイルでは、Strsafe.h には、これらの関数のプロトタイプが含まれています。 そのファイルと、関連するライブラリは Windows SDK の使用です。 Strsafe.h の詳細については、次を参照してください。 [Strsafe.h 関数を使用して](https://go.microsoft.com/fwlink/p/?linkid=165522)します。

一連のカーネル モードの安全な文字列関数は、次の 2 つのサブセットで構成されます。

-   [Unicode と ANSI 文字の安全な文字列関数](https://msdn.microsoft.com/library/windows/hardware/ff563642)

    これらの各関数は、2 バイト Unicode 文字をサポートする W サフィックス付きのバージョンと 1 バイトの ANSI 文字をサポートする A サフィックス付きのバージョンで使用できます。 たとえば、 [ **RtlStringCbCatN**](https://msdn.microsoft.com/library/windows/hardware/ff562801)、2 つの文字列を連結および追加の文字列の長さを制限するは**RtlStringCbCatNW**と**RtlStringCbCatNA**します。

-   [UNICODE の安全な文字列関数\_文字列の構造体](https://msdn.microsoft.com/library/windows/hardware/ff563644)

    これらの各関数を受け入れる、 [ **UNICODE\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff564879)を入力または出力パラメーターまたはその両方として構造体。 たとえば、 [ **RtlStringCbCopyUnicodeString** ](https://msdn.microsoft.com/library/windows/hardware/ff562815)入力パラメーターとして構造体を受け入れる[ **RtlUnicodeStringCopyString** ](https://msdn.microsoft.com/library/windows/hardware/ff562948)出力パラメーターとして構造体を受け入れると[ **RtlUnicodeStringCopy** ](https://msdn.microsoft.com/library/windows/hardware/ff562942)入力と出力の両方のパラメーターとして構造体を受け入れます。

カーネル モードの安全な文字列関数は、次の機能を提供します。

-   安全な文字列の各関数は、入力として、コピー先バッファーのサイズを受け取ります。 関数は、バッファーの末尾を越えた書き込みませんしたがって保証できます。

-   操作が意図した結果を切り捨てます場合でも、Unicode と ANSI 文字列関数は NULL 文字では、すべての出力文字列を終了します。

-   すべての安全な文字列関数は、可能な成功コードを 1 つだけで、NTSTATUS 値を返す (ステータス\_成功した場合)。

-   ほとんどの安全な文字列関数は、バイト カウントと文字カウントされたバージョンの両方で使用できます。 たとえば、 [ **RtlStringCbCat** ](https://msdn.microsoft.com/library/windows/hardware/ff562795)バイト数の 2 つの文字列を連結しますおよび[ **RtlStringCchCat** ](https://msdn.microsoft.com/library/windows/hardware/ff562834) 2 つを連結します。文字列の文字カウントされます。

-   ほとんどの安全な文字列関数の追加機能を提供する拡張、Ex サフィックス付きのバージョンで利用できます。 たとえば、 [ **RtlStringCbCatEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562799)の機能を拡張[ **RtlStringCbCat**](https://msdn.microsoft.com/library/windows/hardware/ff562795)します。

ここでは、次のトピックについて説明します。

[カーネル モードの安全な文字列関数の概要](summary-of-kernel-mode-safe-string-functions.md)

[カーネル モードの安全な文字列関数をインポートします。](importing-kernel-mode-safe-string-functions.md)

 

 





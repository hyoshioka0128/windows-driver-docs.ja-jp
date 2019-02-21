---
title: 符号拡張
description: 符号拡張
ms.assetid: 58e84d09-ab70-4cb2-b12f-4addb34f69d6
keywords:
- 数値の符号拡張
- レジスタの符号拡張
- 符号拡張の MASM 式
- レジスタ、符号拡張
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bda170b255d20262e20db0cfc2be783f5ce4449
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536048"
---
# <a name="sign-extension"></a>符号拡張


## <span id="ddk_sign_extension_dbg"></span><span id="DDK_SIGN_EXTENSION_DBG"></span>


32 ビット符号付き整数が負の場合、最上位ビットは 1 つになります。 この 32 ビット符号付き整数が 64 ビットの数値にキャストされる、上位ビットはゼロ (保存、符号なし整数と番号の 16 進数の値) に設定できます。 または上位ビットを 1 つ (数の符号付きの値を保持) に設定できます。 後者の場合と呼ばれる*拡張機能をサインイン*します。

デバッガーでは、番号を表示するときと C++ の式での MASM 式の符号拡張用の別の規則に従います。

### <a name="span-idsignextensioninmasmexpressionsspanspan-idsignextensioninmasmexpressionsspansign-extension-in-masm-expressions"></a><span id="sign_extension_in_masm_expressions"></span><span id="SIGN_EXTENSION_IN_MASM_EXPRESSIONS"></span>MASM 式の符号拡張

数値を自動的には、特定の条件下で*符号拡張*MASM の式エバリュエーターでします。 符号拡張 0 xffffffff を 0x80000000 からの値のみに影響を与えることができます。 符号拡張機能、高の 32 ビットで書き込むことができる数値のみに影響はビットを 1 に等しかった。

0x12345678 番号が 0x00000000 を常にです\`12345678 とき、デバッガーは 64 ビットの数値として処理します。 その一方で、0x890ABCDE は、64 ビット値として扱われますがときに、残る可能性があります 0x00000000\`890ABCDE または MASM 式エバリュエーターの署名が 0 xffffffff に拡張する\`890ABCDE します。

0 xffffffff を 0x80000000 からの数値は符号拡張、次の条件に基づきます。

-   数値定数は、サインイン ユーザー モードで拡張ことはできません。 カーネル モードで数値定数が符号拡張アクサン グラーブがない限り ( **\`** ) 下位バイトの前にします。 たとえば、カーネル モードでは、16 進数で**EEAA1122**と**00000000EEAA1122**は符号拡張しますが、 **00000000\`EEAA1122**と**0\`EEAA1122**はありません。

-   32 ビット レジスタは両方のモードでの拡張です。

-   擬似レジスタが常に 64 ビット値として格納されます。 拡張が評価されると、サインオンではありません。 擬似レジスタが場合*割り当て*値を使用する式は、標準の C++ 基準に従って評価されます。

-   個別の数値と式でのレジスタは、拡張、記号を指定できますが、他の計算式の評価中には、符号拡張がありません。 その結果、数値の上位ビットをマスクまたは、次の構文を使用して登録できます。
    ```console
    ( 0x0`FFFFFFFF & expression )
    ```

### <a name="span-idsignextensionincexpressionsspanspan-idsignextensionincexpressionsspansign-extension-in-c-expressions"></a><span id="sign_extension_in_c___expressions"></span><span id="SIGN_EXTENSION_IN_C___EXPRESSIONS"></span>C++ の式の符号拡張

デバッガーでは、C++ の式を評価するときは、次の規則が適用されます。

-   レジスタおよび擬似レジスタは、符号拡張ではできません。

-   その他のすべての値は、C++ はその型の値を扱うのとまったく同じに扱われます。

### <a name="span-iddisplayingsignextendedand64bitnumbersspanspan-iddisplayingsignextendedand64bitnumbersspandisplaying-sign-extended-and-64-bit-numbers"></a><span id="displaying_sign_extended_and_64_bit_numbers"></span><span id="DISPLAYING_SIGN_EXTENDED_AND_64_BIT_NUMBERS"></span>符号拡張、および 64 ビットの数値を表示します。

32 ビットと 16 ビットのレジスタ以外のすべての数値として格納されます内部的には、デバッガー内で 64 ビット値。 ただし、数値は、特定の条件を満たす、デバッガーとして表示されますがコマンドの出力で 32 ビットの数値。

デバッガーでは、次の条件を使用して、番号を表示する方法を決定します。

-   数値の上位 32 ビットかすべてゼロ (番号が 0x00000000 の場合は、\`0x00000000 を通じて 00000000\`FFFFFFFF)、デバッガーは、32 ビットの数値として数を表示します。

-   すべての上位 32 ビット数値の場合と下位 32 ビットの最上位ビットが 1 つでもある場合 (、番号は 0 xffffffff から場合に、\`0 xffffffff を 80000000\`FFFFFFFF)、デバッガーは、符号拡張 32 ビットが前提としています。数し、32 ビットの数値として表示されます。

-   前の 2 つの条件が適用されない場合 (0x00000001 からの数がの場合は、\`0 xffffffff を 00000000\`7 fffffff)、デバッガーは、64 ビットの数値として数を表示します。

これらのための規則を表示、番号が 0 xffffffff を 0x80000000 から 32 ビットの数値として表示されたら、上位 32 ビットはすべて 1 または 0 であるかどうかを確認できません。 これら 2 つのケースを区別するためには、(1 つまたは複数の上位ビットをマスクし、結果を表示する) など数に追加の計算を行う必要があります。

 

 






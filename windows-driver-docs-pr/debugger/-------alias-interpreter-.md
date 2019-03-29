---
title: $ (別名インタープリター)
description: ドル記号 ($) 中かっこの後に、さまざまな指定という名前のユーザーのエイリアスに関連する値に評価されます。
ms.assetid: 5182ed99-259e-4e58-8d69-38a702bd8113
keywords:
- $ (別名インタープリター) Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $ (Alias Interpreter)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ebf7173cffb7a3fed01c4e06a97e3ed8529d1c8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579769"
---
# <a name="--alias-interpreter"></a>$ {} (別名インタープリター)


ドル記号の後に中かっこのペア ( **$ {}** )、さまざまな指定という名前のユーザーのエイリアスに関連する値に評価されます。

```dbgcmd

    Text ${Alias} Text 
    Text ${/d:Alias} Text 
    Text ${/f:Alias} Text 
    Text ${/n:Alias} Text 
    Text ${/v:Alias} Text 
```

## <a name="span-idddktokenaliasinterpreterdbgspanspan-idddktokenaliasinterpreterdbgspanparameters"></a><span id="ddk_token_alias_interpreter_dbg"></span><span id="DDK_TOKEN_ALIAS_INTERPRETER_DBG"></span>パラメーター


<span id="Alias"></span><span id="alias"></span><span id="ALIAS"></span>*エイリアス*  
展開または評価するエイリアスの名前を指定します。 *エイリアス*という名前のユーザーのエイリアスである必要がありますまたは*変数*によって使用される値、 [ **.foreach** ](-foreach.md)トークンです。

<span id="_d"></span><span id="_D"></span>**/d**  
エイリアスが現在定義されているかどうかに応じて 1 つまたは 0 に評価されます。 エイリアスが定義されている場合 **${/v:**<em>エイリアス</em>**}** エイリアスが定義されていない場合は、1 に置換されます **${/v:**<em>エイリアス</em>**}** 0 は置き換えられます。

<span id="_f"></span><span id="_F"></span>**/f**  
エイリアスは現在定義されている場合に、エイリアスと同等に評価されます。 エイリアスが定義されている場合 **${/f:**<em>エイリアス</em>**}** エイリアスが定義されていない場合は、エイリアスと同等の; に置換されます **${/f:** <em>エイリアス</em>**}** は空の文字列で置き換えられます。

<span id="_n"></span><span id="_N"></span>**/n**  
エイリアスは現在定義されている場合に、エイリアス名に評価されます。 エイリアスが定義されている場合 **${/n:**<em>エイリアス</em>**}** エイリアスが定義されていない場合は、エイリアス名に置換されます **${/n:** <em>エイリアス</em>**}** は置き換えられませんが、リテラル値を保持 **${/n:**<em>エイリアス</em>**}** します。

<span id="_v"></span><span id="_V"></span>**/v**  
任意のエイリアス評価をできないようにします。 かどうかに関係なく*エイリアス*が定義されている **${/v:**<em>エイリアス</em>**}** のリテラル値を常に保持 **${/v:** <em>エイリアス</em>**}** します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

エイリアスを使用する方法の詳細については、次を参照してください。 [Using エイリアス](using-aliases.md)します。

<a name="remarks"></a>コメント
-------

スイッチが使用されないと、エイリアスが現在定義されている場合 **${**<em>エイリアス</em>**}** エイリアスと同等に置換されます。 スイッチが使用されないと、エイリアスが定義されていない場合 **${**<em>エイリアス</em>**}** のリテラル値を常に保持 **${** <em>エイリアス</em>**}** します。

使用する利点の 1 つ、 **$ {}** トークンは、その他の文字の横にある場合でもにエイリアスを評価することです。 、このトークンを使用せず、スペースでは、その他のトークンから分離されているエイリアスのみがデバッガーに置き換えられます。

状況があるように、場所、 **$ {}** トークンは、何も置き換えられませんが、リテラル値を保持します。 これは、スイッチを使用していない場合に発生と*エイリアス*ときに定義されていない、 **/n**スイッチを使用してと*エイリアス*が定義されていないときに常に、 **/v**スイッチを使用します。 このような場合は、トークンは、ドル記号と中かっこを含め、リテラルの値を保持します。 そのため、これは、コマンドのパラメーターとして使用する場合、構文エラーが発生、しない限り、そのパラメーターは任意のテキスト文字列を受け入れます。

ただし、1 つの例外があります。 使用する場合 **${/v:**<em>エイリアス</em>**}** 最初のパラメーターとして、 [ **(設定の別名) として**](as--as--set-alias-.md)または **(設定の別名) として**コマンドでは、このトークンは、文字列として扱われます*エイリアス*だけで、文字列としてではなく **${/v:**<em>エイリアス</em>**}**. これでのみ動作、**として**、**として**と**ad**コマンド、およびその場合にのみ有効、 **/v**スイッチを使用して、では機能しません **${/n:**<em>エイリアス</em>**}** または **${**<em>エイリアス</em>**}** ときに、リテラル値を保持します。

*エイリアス*という名前のユーザーのエイリアスである必要がありますまたは*変数*によって使用される値、 [ **.foreach** ](-foreach.md)トークン-固定名のエイリアスではありません。 文字列内の固定名のエイリアスがあるかどうかは*エイリアス*、前に置き換えられます、 **$ {}** トークンを評価します。

 

 






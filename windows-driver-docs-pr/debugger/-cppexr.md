---
title: cppexr
description: Cppexr 拡張機能によって、 C++例外レコードの内容が表示されます。
ms.assetid: 568c98e9-31d9-4c49-9b7a-bc8eccfed24a
keywords:
- 例外レコード
- cppexr Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cppexr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff22aa889368d13e27baa86891df6b2f32e298a1
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025272"
---
# <a name="cppexr"></a>!cppexr


**! Cppexr**拡張機能は、 C++例外レコードの内容を表示します。

```dbgsyntax
    !cppexr Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
表示するC++例外レコードのアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext .dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

例外の詳細については、「[例外とイベントの制御](controlling-exceptions-and-events.md)」、「Windows Driver KIT (WDK)」のドキュメント、Windows SDK のドキュメント」、および「 *Microsoft Windows の内部構造*(Mark Russinovich と David ソロモン)」を参照してください。 他の例外レコードを表示するには、 [ **. exr**](-exr--display-exception-record-.md)コマンドを使用します。

<a name="remarks"></a>コメント
-------

**! Cppexr**拡張機能には、例外コード、例外C++のアドレス、例外フラグなど、ターゲットが検出した例外に関連する情報が表示されます。 この例外は、Msvcrt.dll で定義さC++れている標準の例外の1つである必要があります。

通常、 *Address*パラメーターを取得するには、 [ **! analyze-v**](-analyze.md)コマンドを使用します。

**! Cppexr**拡張機能は、 C++例外の種類を特定するのに役立ちます。

 

 






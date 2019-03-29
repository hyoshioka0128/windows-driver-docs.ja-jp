---
title: cppexr
description: Cppexr 拡張機能には、C++ 例外レコードの内容が表示されます。
ms.assetid: 568c98e9-31d9-4c49-9b7a-bc8eccfed24a
keywords:
- 例外レコード
- Windows デバッグ cppexr
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cppexr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 327c2e2ab4bfde70b0363f6d66e48fdf1d1e9820
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580031"
---
# <a name="cppexr"></a>!cppexr


**! Cppexr**拡張機能は、C++ 例外レコードの内容を表示します。

```dbgsyntax
    !cppexr Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示する C++ 例外レコードのアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

例外の詳細については、次を参照してください[を制御する例外とイベント](controlling-exceptions-and-events.md)、Windows Driver Kit (WDK) ドキュメント、Windows SDK のドキュメントと*Microsoft Windows internals 』* マーク。Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)使用して、 [ **.exr** ](-exr--display-exception-record-.md)他の例外レコードを表示するコマンド。

<a name="remarks"></a>コメント
-------

**! Cppexr**拡張機能には、ターゲットが検出されると、例外コード、例外と例外フラグのアドレスを含む C++ 例外に関連する情報が表示されます。 この例外は、Msvcrt.dll で定義されている標準の C++ 例外のいずれかを指定する必要があります。

通常取得することができます、*アドレス*パラメーターを使用して、 [ **! 分析-v** ](-analyze.md)コマンド。

**! Cppexr**拡張機能は C++ 例外の種類を決定するために便利です。

 

 






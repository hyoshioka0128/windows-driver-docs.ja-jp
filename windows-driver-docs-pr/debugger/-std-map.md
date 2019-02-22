---
title: std_map
description: Std_map 拡張機能には、標準マップのツリーのエントリが表示されます。
ms.assetid: 7a921226-e7b1-4c3f-9732-c53c66710ccb
keywords:
- Windows デバッグ std_map
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- std_map
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ddfd3297c1539096b9fb6980cb7d48539a6ba0b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539292"
---
# <a name="stdmap"></a>! std\_マップ


**! Std\_マップ**拡張機能には、std::map ツリーのエントリが表示されます。

```dbgcmd
!std_map Address [Module!Type [TypeSize]]
!std_map -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示する std::map ツリーのアドレスを指定します。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
データ構造が定義されているモジュールを指定します。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *型*   
データ構造の名前を指定します。 これで表現する必要があります<em>モジュール</em>**! std::pair&lt;**<em>Type1</em>**、**<em>Type2</em> **&gt;** フォーム。 場合、*文字サイズ*パラメーターを使用すると、このパラメーターを引用符で囲む必要があります。

<span id="_______TypeSize______"></span><span id="_______typesize______"></span><span id="_______TYPESIZE______"></span> *文字サイズ*   
シンボルを明確にデータ構造体のサイズを指定します。

<span id="_______-_______"></span> **-?**   
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

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

その他の標準テンプレート ライブラリ (STL) を表示する定義済みのテンプレートを参照してください[ **! stl**](-stl.md)します。

<a name="remarks"></a>注釈
-------

など、<em>モジュール</em>**!**<em>型</em>オプションでは、各エントリをテーブル内の指定された型を持つものとして解釈します。

使用[ **dt ve (モジュール! std::pair&lt;Type1、Type2&gt;)** ](dt--display-type-.md)使用可能なサイズを表示します。

 

 






---
title: rtlavl
description: Rtlavl 拡張機能には、RTL_AVL_TABLE 構造体のエントリが表示されます。
ms.assetid: b1e19b13-8bb6-4f40-8d51-368fafc38ebc
keywords:
- avl テーブル
- Windows デバッグ rtlavl
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rtlavl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 172382e4e4aadef1ec61372368a3489e92703bda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560588"
---
# <a name="rtlavl"></a>! rtlavl


**! Rtlavl**拡張機能は、右から左へのエントリを表示します。\_AVL\_テーブルの構造体。

```dbgcmd
!rtlavl Address [Module!Type]
!rtlavl -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
RTL のアドレス指定\_AVL\_を表示するテーブル。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
データ構造が定義されているモジュールを指定します。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *型*   
データ構造の名前を指定します。

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

使用して、 [ **! gentable** ](-gentable.md) AVL テーブルを表示する拡張機能。

<a name="remarks"></a>注釈
-------

など、<em>モジュール</em>**!**<em>型</em>オプションでは、各エントリをテーブル内の指定された型を持つものとして解釈します。

表示は、(WinDbg) では、CTRL + BREAK または (KD、CDB で) CTRL + C を押して、いつでも中断できます。

 

 






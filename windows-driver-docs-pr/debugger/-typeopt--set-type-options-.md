---
title: .typeopt (型のオプションの設定)
description: .Typeopt コマンドを設定または型のオプションが表示されます。
ms.assetid: 17842897-26e3-4b61-aa65-e5cfe8576324
keywords:
- .typeopt (セットの種類のオプション) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .typeopt (Set Type Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85db79a1a1d3d29017c16c103463df926cb9bd5b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334174"
---
# <a name="typeopt-set-type-options"></a>.typeopt (型のオプションの設定)


**.Typeopt**コマンドを設定または型のオプションが表示されます。

```dbgcmd
.typeopt +Flags 
.typeopt -Flags 
.typeopt +FlagName 
.typeopt -FlagName 
.typeopt 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="______________"></span> **+**   
指定された種類のオプションと、 *FlagName*を設定します。

<span id="_______-______"></span> **-**   
指定された種類のオプションと、 *FlagName*クリアします。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
変更の種類のオプションを指定します。 *FlagName* (既定値はありません)、次の値のいずれかの合計を指定できます。

<span id="0x1"></span><span id="0X1"></span>**0x1**  
値は、すべてのウォッチ ウィンドウ、UNICODE データ型を持つものとして [ローカル] ウィンドウで表示されます。

<span id="0x2"></span><span id="0X2"></span>**0x2**  
値は、すべてのウォッチ ウィンドウと LONG データ型として [ローカル] ウィンドウで表示されます。

<span id="0x4"></span><span id="0X4"></span>**0x4**  
すべてのウォッチ ウィンドウと既定の基数で [ローカル] ウィンドウで、整数を表示します。

<span id="0x8"></span><span id="0X8"></span>**0x8**  
デバッガー、[ローカル] ウィンドウまたは [ウォッチ] ウィンドウは、名前でシンボルを参照しますが、この名前に一致する 1 つ以上のシンボルがあるときに、最大サイズと一致するシンボルを選択するとします。 シンボルのサイズが次のように定義されている: シンボルは、関数の名前が場合のサイズは、メモリ内の関数のサイズ。 それ以外の記号のサイズはそれが表すデータ型のサイズです。

<span id="_______FlagName______"></span><span id="_______flagname______"></span><span id="_______FLAGNAME______"></span> *FlagName*   
変更の種類のオプションを指定します。 *FlagName* (既定値はありません)、次の文字列のいずれかを指定できます。

<span id="uni"></span><span id="UNI"></span>**uni**  
値は、すべてのウォッチ ウィンドウ、UNICODE データ型を持つものとして [ローカル] ウィンドウで表示されます。 (これと同じ効果を持つ**0x1**)。

<span id="longst"></span><span id="LONGST"></span>**longst**  
値は、すべてのウォッチ ウィンドウと LONG データ型として [ローカル] ウィンドウで表示されます。 (これと同じ効果を持つ**0x2**)。

<span id="radix"></span><span id="RADIX"></span>**基数**  
すべてのウォッチ ウィンドウと既定の基数で [ローカル] ウィンドウで、整数を表示します。 (これと同じ効果を持つ**0x4**)。

<span id="size"></span><span id="SIZE"></span>**サイズ**  
デバッガー、[ローカル] ウィンドウまたは [ウォッチ] ウィンドウは、名前でシンボルを参照しますが、この名前に一致する 1 つ以上のシンボルがあるときに、最大サイズと一致するシンボルを選択するとします。 シンボルのサイズが次のように定義されている: シンボルは、関数の名前が場合のサイズは、メモリ内の関数のサイズ。 それ以外の記号のサイズはそれが表すデータ型のサイズです。 (これと同じ効果を持つ**0x8**)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

任意の引数を指定せず **.typeopt**現在のシンボルのオプションが表示されます。

 

 






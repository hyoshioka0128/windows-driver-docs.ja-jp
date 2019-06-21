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
ms.openlocfilehash: cdf33bf31c7e45f0375b467675cc040db9ee910a
ms.sourcegitcommit: 0d684828f1cabcde6c4f87bec7d9451997f2fa8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67302035"
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
によって指定された型のオプションと、*フラグ*または*FlagName*を設定します。

<span id="_______-______"></span> **-**    
によって指定された型のオプションと、*フラグ*または*FlagName*クリアします。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
変更の種類のオプションを指定します。 *フラグ*(既定値はありません)、次の値のいずれかの合計を指定できます。

<span id="0x1"></span><span id="0X1"></span>**0x1**  
すべてのウォッチ ウィンドウ、UNICODE データ型を持つものとして [ローカル] ウィンドウで 16 ビット符号なし整数値を表示します。

<span id="0x2"></span><span id="0X2"></span>**0x2**  
表示は、すべてのウォッチ ウィンドウと [ローカル] ウィンドウで 32 ビット整数値を既定の基数の符号なし整数として署名。

<span id="0x4"></span><span id="0X4"></span>**0x4**  
既定の基数での符号なしの値としての符号付きすべてのウォッチ ウィンドウと [ローカル] ウィンドウで、あらゆる規模の整数を表示します。

<span id="0x8"></span><span id="0X8"></span>**0x8**  
デバッガー、[ローカル] ウィンドウまたは [ウォッチ] ウィンドウは、名前でシンボルを参照しますが、この名前に一致する 1 つ以上のシンボルがあるときに、最大サイズと一致するシンボルを選択するとします。 シンボルのサイズが次のように定義されている: シンボルは、関数の名前が場合のサイズは、メモリ内の関数のサイズ。 それ以外の記号のサイズはそれが表すデータ型のサイズです。

<span id="_______FlagName______"></span><span id="_______flagname______"></span><span id="_______FLAGNAME______"></span> *FlagName*   
変更の種類のオプションを指定します。 *FlagName* (既定値はありません)、次の文字列のいずれかを指定できます。

<span id="uni"></span><span id="UNI"></span>**uni**  
すべてのウォッチ ウィンドウ、UNICODE データ型を持つものとして [ローカル] ウィンドウで 16 ビット符号なし整数値を表示します。 (これと同じ効果を持つ**0x1**)。

<span id="longst"></span><span id="LONGST"></span>**longst**  
表示は、すべてのウォッチ ウィンドウと [ローカル] ウィンドウで 32 ビット整数値を既定の基数の符号なし整数として署名。 (これと同じ効果を持つ**0x2**)。

<span id="radix"></span><span id="RADIX"></span>**基数**  
既定の基数での符号なしの値としての符号付きすべてのウォッチ ウィンドウと [ローカル] ウィンドウで、あらゆる規模の整数を表示します。 (これと同じ効果を持つ**0x4**)。

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

既定の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。

 






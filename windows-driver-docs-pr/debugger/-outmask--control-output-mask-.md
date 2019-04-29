---
title: .outmask (出力マスクの制御)
description: .Outmask コマンドでは、現在の出力のマスクを制御します。
ms.assetid: a925f948-a746-4fed-9ccd-95513f41e3bf
keywords:
- コマンドの出力のマスク (.outmask) の制御します。
- .outmask (出力の制御マスク) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .outmask (Control Output Mask)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 953176c909b580c2d04b0305c1d690755a6c453f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334429"
---
# <a name="outmask-control-output-mask"></a>.outmask (出力マスクの制御)


**.Outmask**コマンドは、現在のマスクの出力を制御します。

```dbgcmd
.outmask[-] [/l] Expression 
.outmask /a 
.outmask /d
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
マスクを追加するフラグを指定します。 *式*ULONG するフラグのビットを指定する値を指定できます。 使用できるフラグの一覧は、「解説」セクションの表を参照してください。

<span id="_______-______"></span> **-**   
ビットを削除する*式*マスクに追加することではなく、マスクからを指定します。

<span id="________l______"></span><span id="________L______"></span> **/l**   
現在のログ ファイルの出力のマスクの値を保持します。 含めない場合 **/l**マスクは、標準出力マスクと同じログ ファイルの出力します。

<span id="________a______"></span><span id="________A______"></span> **/a**   
すべてのマスク フラグを有効にします。 このパラメーターは **.outmask 0 xffffffff**します。

<span id="________d______"></span><span id="________D______"></span> **/d**   
既定値には、出力のマスクを復元します。 このパラメーターは **.outmask 0x3F7**します。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

各出力マスク フラグにより、デバッガーで特定の出力を表示する、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。 すべてのマスク フラグを設定すると、すべての出力が表示されます。

デバッガーの出力を読み込むことができないため、慎重マスク フラグを出力を削除する必要があります。

次のフラグ値が存在します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">既定の設定</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>通常の出力</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>エラー出力</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>警告</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>追加の出力</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>プロンプトの出力</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>プロンプトの前に、レジスタのダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>拡張機能の操作に固有の警告</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>デバッグ ターゲットの出力を (たとえば、 <strong>OutputDebugString</strong>または<strong>による DbgPrint</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>デバッグ対象が予期する入力 (たとえば、 <strong>DbgPrompt</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>メッセージのシンボル (たとえば、 <strong>! sym ノイズの多い</strong>)</p></td>
</tr>
</tbody>
</table>

 

 

 






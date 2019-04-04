---
title: .suspend_ui (中断 WinDbg インターフェイス)
description: .Suspend_ui コマンドには、WinDbg デバッグ情報の windows の更新が中断します。
ms.assetid: 7fa6ca5c-f960-49eb-b6f0-a6f2d454984f
keywords:
- .suspend_ui (WinDbg インターフェイスを中断) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .suspend_ui (Suspend WinDbg Interface)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27f259a66db96243b6bdb95910189d4747cb1ed1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552825"
---
# <a name="suspendui-suspend-windbg-interface"></a>明解\_ui (中断 WinDbg インターフェイス)


**明解\_ui**コマンド WinDbg のデバッグ情報のウィンドウの更新を中断します。

```dbgcmd
.suspend_ui 0 
.suspend_ui 1 
.suspend_ui 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______0______"></span> **0**   
WinDbg のデバッグ情報の windows の更新を中断します。

<span id="_______1______"></span> **1**   
WinDbg のデバッグ情報の windows の更新を有効にします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

このコマンドは、WinDbg でのみ使用でき、スクリプト ファイルでは使用できません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

デバッグ情報のウィンドウについては、[デバッグ情報の Windows を使用して](using-debugging-information-windows.md)を参照してください。

<a name="remarks"></a>注釈
-------

任意のパラメーターを指定せず**明解\_ui**デバッグ情報のウィンドウが現在中断されているかどうかが表示されます。

既定では、デバッグ情報のウィンドウは、情報が更新されたたびに、変更結果を表示します。

これらのウィンドウの更新を中断する高速化できます WinDbg クイック操作のシーケンス中に、トレース出力または立て続けに何度もをステップ実行時にします。

 

 






---
title: .netsyms (無効にするネットワークのシンボルの読み込み中)
description: .netsyms (無効にするネットワークのシンボルの読み込み中)
ms.assetid: 09347909-47C8-4a4d-8246-C32A1791F46B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7a6eea7941550e08ef5d10a8f1c942b73266440
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552898"
---
# <a name="netsyms-disable-network-symbol-loading"></a>.netsyms (無効にするネットワークのシンボルの読み込み中)


## <span id="ddk_apc_meta_netsyms_dbg"></span><span id="DDK_APC_META_NETSYMS_DBG"></span>


ネットワーク パスからシンボルを読み込みを許可または拒否するには、.netsyms コマンドを使用します。

### <a name="span-idkdsyntaxspanspan-idkdsyntaxspansyntax"></a><span id="kd_syntax"></span><span id="KD_SYNTAX"></span>構文

**.netsyms** *{yes|no}*

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター

<span id="yes"></span><span id="YES"></span>*うん*  
ネットワークのシンボルの読み込みを有効にします。 これが既定値です。

<span id="no"></span><span id="NO"></span>*違います*  
ネットワークのシンボルの読み込みを無効にします。

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

 

### <a name="span-idremarksspanspan-idremarksspanremarks"></a><span id="remarks"></span><span id="REMARKS"></span>「解説」

引数なしで .netsyms を使用すると、この設定の現在の状態を表示します。

使用[ **! sym ノイズの多い**](-sym.md)または *-n* [ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)として追加の詳細を表示するにはシンボルが読み込まれます。

 

 






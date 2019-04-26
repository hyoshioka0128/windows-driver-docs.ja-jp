---
title: .force_tb (分岐のトレースを強制的に許可)
description: .Force_tb コマンドには、ブート プロセスの早い段階でのトレースの分岐にプロセッサがにより適用されます。
ms.assetid: ac4aabfa-6d00-4478-9c13-213bf89f613a
keywords:
- .force_tb (ブランチのトレースを強制的に許可する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .force_tb (Forcibly Allow Branch Tracing)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9ec13cd9f4e87654e952746a81d5e4df6b3f282c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336711"
---
# <a name="forcetb-forcibly-allow-branch-tracing"></a>.force\_tb (強制的に許可するブランチ トレース)


**.Force\_tb**コマンド プロセッサ ブート プロセスの早い段階で分岐をトレースするように強制します。

```dbgcmd
.force_tb 
```

## <span id="ddk_meta_forcibly_allow_branch_tracing_dbg"></span><span id="DDK_META_FORCIBLY_ALLOW_BRANCH_TRACING_DBG"></span>


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

通常、デバッガー プロセッサ制御ブロック (PRCB) が初期化された後は、ブランチのトレースが有効にします。 この初期化は、ブート プロセスの早い段階で発生します。

ただし、使用する必要がある場合、 [ **tb (トレースを次の分岐)** ](tb--trace-to-next-branch-.md)この初期化の前にコマンドを使用することができます、 **.force\_tb**分岐を有効にするコマンド以前のトレース。 プロセッサの状態を破損することがあるために、このコマンドを慎重に使用します。

 

 






---
title: ~ s (変更の現在のプロセッサ)
description: ~ S コマンドは、マルチプロセッサ システムでプロセッサがデバッグを設定します。カーネル モードで ~ s が、現在のプロセッサを変更します。
ms.assetid: bd036a25-1e3c-4b57-9c7c-5f1730008cd7
keywords:
- 現在のプロセッサを変更 (~ s) コマンド
- マルチプロセッサ コンピューターで、変更の現在のプロセッサ (~ s) コマンド
- プロセッサ
- ~ s (現在のプロセッサを変更する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~s (Change Current Processor)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 30b4e8cc1a59cfb25f6485536b4d88b8bc146b75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557026"
---
# <a name="s-change-current-processor"></a>~ s (変更の現在のプロセッサ)


**~ S**コマンドは、マルチプロセッサ システムでプロセッサがデバッグを設定します。

カーネル モードで **~ s**現在のプロセッサを変更します。 このコマンドを混同しないでください、 [ **~ (設定現在のスレッド) s** ](-s--set-current-thread-.md) (これは、ユーザー モードでのみ機能します) のコマンドを[ **| s (現在のプロセスの設定)** ](-s--set-current-process-.md)コマンド、 [ **| |s (現在のシステムの設定)** ](--s--set-current-system-.md)コマンド、または[ **s (メモリの検索)** ](s--search-memory-.md)コマンド。

```dbgcmd
~Processor s
```

## <a name="span-idddkcmdchangecurrentprocessordbgspanspan-idddkcmdchangecurrentprocessordbgspanparameters"></a><span id="ddk_cmd_change_current_processor_dbg"></span><span id="DDK_CMD_CHANGE_CURRENT_PROCESSOR_DBG"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
デバッグするプロセッサの数を指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロセッサは、カーネル モードでのみ指定できます。 ユーザー モードでは、チルダ (~) は、スレッドを指します。

プロンプトのデバッグ、カーネルの形状で複数のプロセッサ システムで作業しているときにすぐにわかります。 次の例では、0: コンピューターの最初のプロセッサをデバッグしていることを意味します。

```dbgcmd
0: kd>
```

次のコマンドを使用して、プロセッサ間で切り替えます。

```dbgcmd
0: kd> ~1s
1: kd>
```

ここで 2 番目のプロセッサがデバッグされているコンピューターで。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[マルチプロセッサの構文](multiprocessor-syntax.md)

 

 







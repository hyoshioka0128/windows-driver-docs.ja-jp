---
title: .wake (デバッガーのスリープ解除)
description: .Wake コマンドは、スリープ モードを終了します。 このコマンドは、カーネル デバッガーからユーザー モード デバッガーの制御を行う場合にのみに使用されます。
ms.assetid: 01aead7e-1f46-46cf-a697-ab5ff6329ac7
keywords:
- デバッガー (.wake) コマンドをスリープ解除します。
- カーネル デバッガー Wake デバッガー (.wake) コマンドからユーザー モード デバッガーの制御
- .wake (ウェイク デバッガー) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .wake (Wake Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 30ae68fce209bb88acec21b488ebf8d053e76589
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581999"
---
# <a name="wake-wake-debugger"></a>.wake (デバッガーのスリープ解除)


**.Wake**原因スリープ モードを終了させるコマンド。 このコマンドは、カーネル デバッガーからユーザー モード デバッガーの制御を行う場合にのみに使用されます。

```dbgcmd
.wake PID
```

## <a name="span-idddkmetawakedebuggerdbgspanspan-idddkmetawakedebuggerdbgspanparameters"></a><span id="ddk_meta_wake_debugger_dbg"></span><span id="DDK_META_WAKE_DEBUGGER_DBG"></span>パラメーター


<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
ユーザー モード デバッガーのプロセス ID。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル デバッガーからユーザー モード デバッガーの制御</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)を参照してください。 デバッガーのプロセス ID を検索する方法については、[プロセス ID の検索](finding-the-process-id.md)を参照してください。

<a name="remarks"></a>コメント
-------

カーネル デバッガーからユーザー モード デバッガーの制御を行うと、システムがスリープ モードでは、このコマンドはスリープ タイマーが切れる前に、デバッガーを稼動状態に使用できます。

ターゲット コンピューターでは、ユーザー モード デバッガーにも、ホスト コンピューター上のカーネル デバッガーには、このコマンドは発行されません。 3 番目のデバッガー (KD、CDB、または NTSD) から発行する必要がありますが、ターゲット コンピューターで実行されています。

このデバッガーでは、この目的で明示的に開始するか、実行されるように別のデバッガーができます。 ただし、既に実行されているその他のデバッガーがない場合は、方が簡単で CDB を使用するだけ、 **-wake** [**コマンド ライン オプション**](cdb-command-line-options.md)します。

 

 






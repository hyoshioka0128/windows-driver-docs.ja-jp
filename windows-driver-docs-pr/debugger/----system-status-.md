---
title: (システム状態)
description: 二重の垂直 () のコマンド バーでは、指定したシステムまたは現在デバッグ中のすべてのシステムのステータスを出力します。(プロセスの状態) コマンドを使用してこのコマンドを混同しないでください。
ms.assetid: fcea61b1-2ec5-4c80-abd7-269b95d56cd4
keywords:
- (システム状態)Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- (System Status)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e9c35c30ae28f7610712d02c114f19aa2b24027
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337066"
---
# <a name="-system-status"></a>|| (システム ステータス)


二重の縦棒 ( **||** ) コマンドは、指定したシステムまたは現在デバッグ中のすべてのシステム状態を出力します。

このコマンドを混同しないでください、 [ **|(プロセスの状態)** ](---process-status-.md)コマンド。

```dbgcmd
|| System 
```

## <a name="span-idddkcmdsystemstatusdbgspanspan-idddkcmdsystemstatusdbgspanparameters"></a><span id="ddk_cmd_system_status_dbg"></span><span id="DDK_CMD_SYSTEM_STATUS_DBG"></span>パラメーター


<span id="_______System______"></span><span id="_______system______"></span><span id="_______SYSTEM______"></span> *システム*   
表示するシステムを指定します。 このパラメーターを省略した場合は、デバッグしているすべてのシステムが表示されます。 構文の詳細については、次を参照してください。[システム構文](system-syntax.md)します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>複数のターゲットのデバッグ</p></td>
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

**||** コマンドは、複数のターゲットをデバッグする際にのみ役立ちます。 すべてではなく、多くの複数ターゲットのデバッグ セッションには、複数のシステムが含まれます。 これらのセッションに関する詳細については、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。

各システムの一覧には、サーバー名およびプロトコルの詳細が含まれています。 デバッガーが実行されているシステムとして識別 **&lt;ローカル&gt;** します。

次の例では、このコマンドを使用する方法を示します。 次のコマンドでは、すべてのシステムが表示されます。

```dbgcmd
3:2:005> ||
```

次のコマンドでは、すべてのシステムも表示されます。

```dbgcmd
3:2:005> ||*
```

次のコマンドは、現在アクティブなシステムを表示します。

```dbgcmd
3:2:005> ||.
```

次のコマンドでは、最新の例外や中断があったシステムが表示されます。

```dbgcmd
3:2:005> ||#
```

次のコマンドでは、システム番号 2 が表示されます。

```dbgcmd
3:2:005> ||2
```

 

 






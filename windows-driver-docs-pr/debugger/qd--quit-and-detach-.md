---
title: qd (Quit およびデタッチ)
description: Qd コマンドでは、デバッグ セッションを終了し、実行されているすべてのユーザー モード ターゲット アプリケーションのまま。
ms.assetid: 3282c78b-6c4b-4c1b-a086-4890c3140ab9
keywords:
- qd (Quit およびデタッチ) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- qd (Quit and Detach)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0a1c615d108c8af8319764af5beb651255da28d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531748"
---
# <a name="qd-quit-and-detach"></a>qd (Quit およびデタッチ)


**Qd**コマンドは、デバッグ セッションを終了し、ユーザー モードのターゲット アプリケーションの実行中のままです。 (CDB および KD では、このコマンドも、デバッガーを終了自体。 、WinDbg で次のコマンドを返します、デバッガー休止モードにします。)

```dbgcmd
qd 
```

## <span id="ddk_cmd_quit_and_detach_dbg"></span><span id="DDK_CMD_QUIT_AND_DETACH_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**Qd**コマンドは、対象アプリケーションからデタッチし、まま、ターゲットがまだ実行中、デバッグ セッションは終わります。 ただし、このコマンドは Microsoft Windows XP と Windows の以降のバージョンでのみサポートされています。 Windows 2000 では、 **qd**警告メッセージを生成し、影響を与えません。

使用することはできません、デバッガーのリモート デバッグを実行するとき、 **qd**デバッグ クライアントからコマンド。

 

 






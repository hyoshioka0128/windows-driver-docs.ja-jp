---
title: q、qq (終了)
description: Q と qq コマンドでは、デバッグ セッションを終了します。
ms.assetid: 94d35997-8b21-4d25-b2ae-4b2a78240153
keywords:
- q、qq (終了) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- q, qq (Quit)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1bfe9421c9da02d26bbbc58b3794de108c53093e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362382"
---
# <a name="q-qq-quit"></a>q、qq (終了)


**Q**と**qq**コマンドは、デバッグ セッションを終了します。 (CDB および KD では、このコマンドも、デバッガーを終了自体。 、WinDbg で次のコマンドを返します、デバッガー休止モードにします。)

```dbgcmd
q 
qq 
```

## <span id="ddk_cmd_quit_dbg"></span><span id="DDK_CMD_QUIT_DBG"></span>


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

ユーザー モードのデバッグで、 **q**コマンドは、デバッグ セッションを終了し、ターゲット アプリケーションを閉じます。

カーネル モードのデバッグで、 **q**コマンドは、ログ ファイルを保存し、デバッグ セッションは終わります。 ターゲット コンピューターがロックされたままにします。

KD でこのコマンドが機能しない場合、以下のキーを押して[ **CTRL + R キーを押しながら ENTER** ](ctrl-r--re-synchronize-.md)デバッガーのキーボードと、再試行してください、 **q**コマンド。 このアクションが機能しない場合は、デバッガーを終了する CTRL + B キーを押しながら ENTER を使用する必要があります。

**Qq**コマンドの動作と同様に、 **q**コマンドをリモート デバッグを実行している場合を除き、します。 リモート デバッグ中、 **q**コマンドには効果がありませんが、 **qq**コマンド デバッグ サーバーが終了します。 この効果の詳細については、次を参照してください。[リモート デバッグで、デバッガー](remote-debugging-through-the-debugger.md)します。

 

 






---
title: .restart (再起動カーネル接続)
description: .Restart コマンドでは、カーネルの接続を再起動します。このコマンドはユーザー モードでのみ動作 .restart (ターゲット アプリケーションの再起動) のコマンドを使用を混同しないでください。
ms.assetid: 2c81625b-d75f-4c5f-9437-9619bf33b500
keywords:
- .restart (再起動カーネル接続) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .restart (Restart Kernel Connection)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b9a57ecd03ed93ca6dc2c2a4f4882737e33f1122
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539123"
---
# <a name="restart-restart-kernel-connection"></a>.restart (再起動カーネル接続)


**.Restart**コマンドは、カーネルの接続を再起動します。

このコマンドを混同しないでください、 [ **.restart (ターゲット アプリケーションの再起動)** ](-restart--restart-target-application-.md)コマンドで、ユーザー モードでのみ機能します。

```dbgcmd
.restart 
```

## <span id="ddk_meta_restart_kernel_connection_dbg"></span><span id="DDK_META_RESTART_KERNEL_CONNECTION_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

使用することができます、 **.restart** KD でのみコマンド。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ターゲットとの接続を再確立の詳細については、[対象のコンピューターに同期](synchronizing-with-the-target-computer.md)を参照してください。

<a name="remarks"></a>注釈
-------

**.Restart**コマンドと似ています、 [ **(再同期) CTRL + R** ](ctrl-r--re-synchronize-.md)点を除いて、コマンド **.restart**でさらに広範なは、効果です。 このコマンドは、デバッガーを終了し、対象のコンピュータに新しいデバッガーをアタッチします。

**.Restart**コマンドは、実行している場合、最も役に立つ[remote.exe を通じてリモート デバッグ](remote-debugging-through-remote-exe.md)デバッガーを再起動して、終了を困難になる可能性があります。 ただし、使用することはできません **.restart**デバッガーからのリモート デバッグを実行している場合、デバッグのクライアントから。

 

 






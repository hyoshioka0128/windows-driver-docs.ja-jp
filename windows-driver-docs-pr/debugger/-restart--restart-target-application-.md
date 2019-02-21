---
title: .restart (ターゲット アプリケーションを再起動)
description: .Restart コマンドでは、ターゲット アプリケーションを再起動します。このコマンドはカーネル モードでのみ動作 .restart (再起動カーネル接続) のコマンドを使用を混同しないでください。
ms.assetid: abfa1817-41d8-4bb2-a6d2-e9c9027b50df
keywords:
- .restart (ターゲット アプリケーションを再起動) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .restart (Restart Target Application)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 77576f22e1ac1fbb039369494a8683ccfa1bb582
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560583"
---
# <a name="restart-restart-target-application"></a>.restart (ターゲット アプリケーションを再起動)


**.Restart**コマンドは、対象のアプリケーションを再起動します。

このコマンドを混同しないでください、 [ **.restart (再起動カーネル接続)** ](-restart--restart-kernel-connection-.md)コマンドで、カーネル モードでのみ動作します。

```dbgcmd
.restart 
```

## <span id="ddk_meta_restart_target_application_dbg"></span><span id="DDK_META_RESTART_TARGET_APPLICATION_DBG"></span>


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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

このコマンドと、関連するコマンドの概要を発行する方法の詳細については、次を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>注釈
-------

CDB と WinDbg は、ターゲット アプリケーションを再起動して、デバッガーが最初に、アプリケーションを作成する場合がします。 使用することができます、 **.restart**コマンドの場合でも、ターゲット アプリケーションが既に閉じられています。

ただし場合は、アプリケーションが実行されていると、デバッガーは、後でプロセスにアタッチ、 **.restart**コマンドが影響を与えません。

プロセスが再起動されると、すぐに、デバッガーを中断します。

WinDbg を使用して、[ビュー |WinDbg コマンド ライン](view---windbg-command-line.md)WinDbg コマンド プロンプトから、ターゲットを開始して、使用するかどうかを決定する前に、このコマンドラインを確認するかどうかにコマンド **.restart**します。

 

 






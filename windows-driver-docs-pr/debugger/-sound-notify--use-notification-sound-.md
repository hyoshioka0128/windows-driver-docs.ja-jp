---
title: .sound_notify (通知音の使用)
description: .Sound_notify コマンドでは、WinDbg 待機-コマンドの状態になったときに再生されるサウンドを実行します。
ms.assetid: 72ef33ea-1c75-4add-80eb-a0d824571948
keywords:
- .sound_notify (通知サウンドを使用して) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .sound_notify (Use Notification Sound)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb846550287246a942cbd36da74bfadf122013a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553035"
---
# <a name="soundnotify-use-notification-sound"></a>.sound\_通知 (音の通知を使用)


**.Sound\_通知**コマンドは、WinDbg 待機-コマンドの状態になったときに再生されるサウンドを実行します。

```dbgcmd
.sound_notify /ed 
.sound_notify /ef File 
.sound_notify /d 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________ed______"></span><span id="________ED______"></span> **/ed**   
WinDbg 待機-コマンドの状態になったときに再生できるように既定の Windows 警告音をによりします。

<span id="________ef_______File______"></span><span id="________ef_______file______"></span><span id="________EF_______FILE______"></span> **/ef** **** *ファイル*   
WinDbg 待機-コマンドの状態になったときに再生できるように指定したファイルに含まれているサウンドをによりします。

<span id="________d"></span><span id="________D"></span> **/d**  
サウンドの再生を無効にします。

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
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

 

 






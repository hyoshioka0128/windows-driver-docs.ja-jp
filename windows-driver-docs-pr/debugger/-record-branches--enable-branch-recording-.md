---
title: .record_branches (ブランチの記録を有効にする)
description: .Record_branches コマンドでは、ターゲットのコード実行の分岐の記録を使用します。
ms.assetid: 522eeba5-b6c5-473c-9c8e-8ef4c941079f
keywords:
- ブランチの記録 (.record_branches) コマンドを有効にします。
- .record_branches (ブランチの記録を有効にする) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .record_branches (Enable Branch Recording)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f06ce24825ac7170f226347d2477d55af9aa6720
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537052"
---
# <a name="recordbranches-enable-branch-recording"></a>.record\_ブランチ (分岐の記録を有効にする)


**.Record\_分岐**コマンド ターゲットのコード実行の分岐の記録は有効にします。

```dbgcmd
.record_branches {1|0} 
.record_branches
```

## <span id="ddk_meta_enable_branch_recording_dbg"></span><span id="DDK_META_ENABLE_BRANCH_RECORDING_DBG"></span>


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
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>x64 ベースのみ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**.Record\_分岐 1**コマンド ターゲットのコード内の分岐の記録は有効にします。 **.Record\_分岐 0**コマンドは、この記録を無効にします。

パラメーターを指定せず **.record\_分岐**この設定の現在の状態が表示されます。

 

 






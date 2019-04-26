---
title: ENTER (最後のコマンドを繰り返す)
description: ENTER キーでは、入力した最後のコマンドが繰り返されます。
ms.assetid: 058e455a-8934-4b28-8cf0-2d3f09a7e7cc
keywords:
- (最後のコマンドを繰り返し) を入力します Windows のデバッグ。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ENTER (Repeat Last Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8bd72fad5a79c949b008ae271f5d89fe0d1e076f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347853"
---
# <a name="enter-repeat-last-command"></a>ENTER (最後のコマンドを繰り返す)


ENTER キーでは、入力した最後のコマンドが繰り返されます。

```dbgcmd
ENTER
```

## <span id="ddk_cmd_repeat_last_command_dbg"></span><span id="DDK_CMD_REPEAT_LAST_COMMAND_DBG"></span>


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

CDB と KD では、以前に入力したコマンドを再発行を単独でコマンド プロンプトで ENTER キーを押します。

、WinDbg で ENTER キーを持たない有効か、を使用して、前のコマンドを繰り返すことができます。 このオプションを設定することができます、**オプション** ダイアログ ボックス。 (を開くには、**オプション**ダイアログ ボックスで、をクリックして**オプション**上、**ビュー** ] メニューの [または] をクリックして、**オプション**ボタン (![スクリーン ショット[オプション] ボタンの](images/tbopt.png)) ツールバー)。

最後のコマンドを繰り返し実行するには ENTER を設定するが、内の空白を作成する場合、[デバッガー コマンド ウィンドウ](debugger-command-window.md)を使用して、 [  **\* (コメント行の指定子)** ](----comment-line-specifier-.md)トークンし、し、ENTER キーを数回押します。

 

 






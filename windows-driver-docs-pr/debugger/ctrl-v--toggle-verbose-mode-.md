---
title: Ctrl + V (詳細モードの切り替え)
description: Ctrl キーを押しながら V キーは、オンとオフ、詳細モードを切り替えます。
ms.assetid: 1aca1452-86dd-4573-8ad0-e46aa474a324
keywords:
- Ctrl キーを押しながら V (詳細モードの切り替え) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+V (Toggle Verbose Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c4ddf221b72862cef4d520fe8e34a7c4524c709
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578544"
---
# <a name="ctrlv-toggle-verbose-mode"></a>Ctrl + V (詳細モードの切り替え)


Ctrl キーを押しながら V キーは、オンとオフ、詳細モードを切り替えます。

CDB/KD 構文

```dbgcmd
CTRL+V  ENTER 
```

WinDbg の構文

```dbgcmd
CTRL+ALT+V 
```

## <span id="ddk_meta_ctrl_v_dbg"></span><span id="DDK_META_CTRL_V_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>デバッガー</strong></p></td>
<td align="left"><p>、KD、CDB WinDbg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

詳細モードをオンにすると (登録のダンプ) などのいくつかの表示コマンドは、さらに詳しい出力を生成します。 デバッガーに送信されるすべてのモジュールの読み込み操作が表示されます。 オペレーティング システムによってドライバーまたは DLL が読み込まれるたびに、デバッガーが通知されます。

WinDbg では、このことができますもすることで実現選択[ビュー |詳細な出力](view---verbose-output.md)します。

 

 






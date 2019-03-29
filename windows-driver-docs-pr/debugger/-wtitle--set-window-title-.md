---
title: .wtitle (ウィンドウ タイトルの設定)
description: .Wtitle コマンドは、WinDbg のメイン ウィンドウで、または NTSD、KD、CDB、ウィンドウのタイトルを設定します。
ms.assetid: 9ff74a70-22fd-4bb7-b124-f262a37cfd1f
keywords:
- .wtitle (セット ウィンドウのタイトル) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .wtitle (Set Window Title)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a92d75bc91a876439c368309cc660acff4bdb25b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580633"
---
# <a name="wtitle-set-window-title"></a>.wtitle (ウィンドウ タイトルの設定)


**.Wtitle** WinDbg のメイン ウィンドウで、または NTSD、KD、CDB、ウィンドウで、コマンドがタイトルを設定します。

```dbgcmd
.wtitle Title 
```

## <a name="span-idddkmetasetwindowtitledbgspanspan-idddkmetasetwindowtitledbgspanparameters"></a><span id="ddk_meta_set_window_title_dbg"></span><span id="DDK_META_SET_WINDOW_TITLE_DBG"></span>パラメーター


<span id="_______Title______"></span><span id="_______title______"></span><span id="_______TITLE______"></span> *タイトル*   
ウィンドウを使用するタイトル。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

このコマンドは、スクリプト ファイルでは使用できません。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

CDB、NTSD、KD の場合、 **.wtitle**コマンドが使用されていない、ウィンドウのタイトルが、デバッガーを起動するために使用するコマンドラインと一致します。

WinDbg の場合は **.wtitle**されていません。 使用すると、メイン ウィンドウのタイトルは、ターゲットの名前が含まれます。 デバッグ サーバーがアクティブである場合も、接続文字列が表示されます。 複数のデバッグ サーバーがアクティブな場合は、最新のものだけが表示されます。

ときに **.wtitle**を使用する*タイトル*この情報はすべて置き換えられます。 デバッグ サーバーが、後で開始された場合でも*タイトル*は変更されません。

WinDbg のバージョン番号は常にこのコマンドを使用するかどうかに関係なく、ウィンドウのタイトル バーに表示されます。

 

 






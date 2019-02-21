---
title: CTRL + W (表示のデバッガー バージョン)
description: CTRL + W キーには、デバッガーと読み込まれたすべての拡張 Dll のバージョン情報が表示されます。
ms.assetid: 9651965e-fbf5-4084-adcd-63de60998b8b
keywords:
- CTRL + W (表示のデバッガー バージョン) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+W (Show Debugger Version)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58c1d4703ecb181a0479cc9b803c21bafa72fd9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559547"
---
# <a name="ctrlw-show-debugger-version"></a>CTRL + W (表示のデバッガー バージョン)


CTRL + W キーには、デバッガーと読み込まれたすべての拡張 Dll のバージョン情報が表示されます。

CDB/KD 構文

```dbgcmd
CTRL+W  ENTER 
```

WinDbg の構文

```dbgcmd
CTRL+ALT+W 
```

## <span id="ddk_meta_ctrl_w_dbg"></span><span id="DDK_META_CTRL_W_DBG"></span>


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

 

<a name="remarks"></a>注釈
-------

同じ効果があります、 [**バージョン (デバッガーのバージョンの表示)** ](version--show-debugger-version-.md)コマンドをする点を除いて、後者が Windows オペレーティング システムのバージョンも表示されます。

WinDbg では、このことができますもすることで実現選択[ビュー |バージョンを表示する](view---show-version.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**バージョン (デバッガーのバージョンの表示)**](version--show-debugger-version-.md)

[**vertarget (ターゲット コンピューター バージョンの表示)**](vertarget--show-target-computer-version-.md)

 

 







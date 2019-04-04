---
title: Ctrl + W (デバッガーのバージョンの表示)
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
ms.openlocfilehash: 6d70f693c518b594259c9d4cb1d15ffd50091977
ms.sourcegitcommit: 672bf3fd18f6c169b5634476613ce1da9250413b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2019
ms.locfileid: "58898059"
---
# <a name="ctrlw-show-debugger-version"></a>Ctrl + W (デバッガーのバージョンの表示)


CTRL + W キーには、デバッガーと読み込まれたすべての拡張 Dll のバージョン情報が表示されます。

CDB/KD 構文

```dbgcmd
CTRL+W  ENTER 
```

WinDbg の構文

```dbgcmd
CTRL+ALT+W 
```


## <a name="environment"></a>環境

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


[**version (デバッガー バージョンの表示)**](version--show-debugger-version-.md)

[**vertarget (ターゲット コンピューター バージョンの表示)**](vertarget--show-target-computer-version-.md)

 

 







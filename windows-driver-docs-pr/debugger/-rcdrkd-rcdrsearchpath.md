---
title: rcdrkd.rcdrsearchpath
description: Rcdrkd.rcdrsearchpath 拡張機能は、トレース メッセージの形式 (TMF) とトレース メッセージのコントロール (TMC) ファイルの検索パスを設定します。
ms.assetid: AB19DC1B-009E-445A-B66B-5CC7EF54086F
keywords:
- デバッグ rcdrkd.rcdrsearchpath Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrsearchpath
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: edf7feb4f5665989db20cac792a09e019697a305
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338947"
---
# <a name="rcdrkdrcdrsearchpath"></a>!rcdrkd.rcdrsearchpath


**! Rcdrkd.rcdrsearchpath**拡張機能は、トレース メッセージの形式 (TMF) とトレースの検索パス メッセージ コントロール (TMC) ファイルを設定します。

```dbgcmd
!rcdrkd.rcdrsearchpath FilePath
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______FilePath______"></span><span id="_______filepath______"></span><span id="_______FILEPATH______"></span> *FilePath*   
形式のファイルへのパス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

<a name="remarks"></a>注釈
-------

このコマンドで設定されている検索パス、トレースで指定された検索パスよりも優先\_形式\_検索\_PATH 環境変数。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[RCDRKD 拡張機能](rcdrkd-extensions.md)

 

 







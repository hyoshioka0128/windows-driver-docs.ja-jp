---
title: logexts.logi
description: Logexts.logi 拡張機能では、ターゲット アプリケーションにロガーを挿入することでログ記録を初期化します。
ms.assetid: c02d2799-c83a-455d-90c0-401244062365
keywords:
- デバッグ logexts.logi Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 45875b0a663aeb83581401216469f04e57bdc800
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336150"
---
# <a name="logextslogi"></a>!logexts.logi


**! Logexts.logi**拡張機能は、ターゲット アプリケーションにロガーを挿入することでログ記録を初期化します。

```dbgcmd
    !logexts.logi [OutputDirectory] 
```

## <a name="span-idddklogextslogidbgspanspan-idddklogextslogidbgspanparameters"></a><span id="ddk__logexts_logi_dbg"></span><span id="DDK__LOGEXTS_LOGI_DBG"></span>パラメーター


<span id="_______OutputDirectory______"></span><span id="_______outputdirectory______"></span><span id="_______OUTPUTDIRECTORY______"></span> *OutputDirectory*   
出力に使用するディレクトリを指定します。 場合*OutputDirectory*指定は、存在する必要があります--、デバッガーは作成されません。 相対パスが指定されている場合、デバッガーの起動元のディレクトリを基準となります。 場合*OutputDirectory*は省略すると、デスクトップへのパスが使用されます。 デバッガーの LogExts サブディレクトリが作成されます*OutputDirectory*、およびすべての Logger 出力をこのサブディレクトリに配置されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。 [Logger と LogViewer](logger-and-logviewer.md)します。

<a name="remarks"></a>注釈
-------

このコマンドは、ログ記録を初期化しますが、実際に有効されません。 ログ記録を有効にできる、 [ **! logexts.loge** ](-logexts-loge.md)コマンド。

 

 






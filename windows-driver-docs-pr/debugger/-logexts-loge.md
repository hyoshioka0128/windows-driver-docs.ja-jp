---
title: logexts.loge
description: Logexts.loge 拡張機能では、ログ記録を有効します。 ログ記録が初期化されていない場合は初期化され、有効になっています。
ms.assetid: d8b621f1-19e7-4c42-a428-8572d29b666f
keywords:
- デバッグ logexts.loge Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.loge
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25d2760977acb60e7351473100a21b3061e4dc80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580476"
---
# <a name="logextsloge"></a>!logexts.loge


**! Logexts.loge**拡張機能で記録できます。 ログ記録が初期化されていない場合は初期化され、有効になっています。

```dbgcmd
    !logexts.loge [OutputDirectory] 
```

## <a name="span-idddklogextslogedbgspanspan-idddklogextslogedbgspanparameters"></a><span id="ddk__logexts_loge_dbg"></span><span id="DDK__LOGEXTS_LOGE_DBG"></span>パラメーター


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

詳細については、[Logger と LogViewer](logger-and-logviewer.md)を参照してください。

<a name="remarks"></a>コメント
-------

かどうかロガーいないまだに挿入された対象アプリケーションを[ **! logexts.logi** ](-logexts-logi.md)拡張機能、 **! logexts.loge**拡張機能は、ターゲットにロガーを挿入し、ログ記録を有効にします。

場合[ **! logexts.logi** ](-logexts-logi.md)が既に実行を含めることはできません*OutputDirectory*出力ディレクトリが既に設定されている、ためです。

 

 






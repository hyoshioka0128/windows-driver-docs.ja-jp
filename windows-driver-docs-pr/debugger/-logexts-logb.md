---
title: logexts.logb
description: Logexts.logb 拡張機能は、表示または出力バッファーをフラッシュします。
ms.assetid: 3c6ec412-f800-469b-9a9f-ebc2940d00fe
keywords:
- デバッグ logexts.logb Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7e3309d55ecfb336e59024e9660dba6c0ff53e32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336189"
---
# <a name="logextslogb"></a>!logexts.logb


**! Logexts.logb**拡張機能を表示または出力バッファーをフラッシュします。

```dbgcmd
!logexts.logb p 
!logexts.logb f 
```

## <a name="span-idddklogextslogbdbgspanspan-idddklogextslogbdbgspanparameters"></a><span id="ddk__logexts_logb_dbg"></span><span id="DDK__LOGEXTS_LOGB_DBG"></span>パラメーター


<span id="_______p______"></span><span id="_______P______"></span> **p**   
デバッガーに表示される出力バッファーの内容をによりします。

<span id="_______f"></span><span id="_______F"></span> **f**  
ディスクに出力バッファーをフラッシュします。

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

<a name="remarks"></a>コメント
-------

パフォーマンスの考慮事項としては、ログ出力は出力バッファーが完全な場合にのみディスクにフラッシュされます。 既定では、バッファーは、2144 バイトです。

**! Logexts.logb p**拡張機能は、デバッガーで、バッファーの内容を表示します。

**! Logexts.logb f**の拡張機能は、ログ ファイルにバッファーをフラッシュします。 バッファー メモリは、対象のアプリケーションで管理されるため、アクセス違反や、ターゲット アプリケーション内の他の回復不能なエラーがある場合、バッファーをディスクの自動の書き込みは発生しません。 このような場合は、手動でディスクにバッファーをフラッシュするこのコマンドを使用する必要があります。 それ以外の場合、最も最近記録された Api 可能性があります、ログ ファイルには表示されません。

 

 






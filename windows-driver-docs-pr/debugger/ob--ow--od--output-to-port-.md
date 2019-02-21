---
title: ob、ow、od (ポートに出力)
description: Ob ow、od コマンドがバイト、単語、またはダブル ワードを選択したポートに送信します。
ms.assetid: 04133df7-4b60-4709-a9e1-5946c8d30f8c
keywords:
- ob、ow、od (出力ポートに) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ob, ow, od (Output to Port)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2123755b3c6904d83624152e3f9f38b79fbc2389
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552060"
---
# <a name="ob-ow-od-output-to-port"></a>ob、ow、od (ポートに出力)


**Ob**、 **ow**、および**od**コマンド バイト、単語、またはダブル ワードを選択したポートに送信します。

```dbgcmd
ob Address Value 
ow Address Value 
od Address Value 
```

## <a name="span-idddkcmdoutputtoportdbgspanspan-idddkcmdoutputtoportdbgspanparameters"></a><span id="ddk_cmd_output_to_port_dbg"></span><span id="DDK_CMD_OUTPUT_TO_PORT_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ポートのアドレスを指定します。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *値*   
ポートに書き込む 16 進数の値を指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>x86 ベースのみ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**Ob**コマンドは、1 バイトを書き込みます、 **ow**コマンドは、単語を書き込みます、 **od**コマンドは、ダブル ワードを書き込みます。

送信することはしない単語、またはダブル ワードがこのサイズはサポートされていないポートにすることを確認します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**ib、id、インフォメーション ワーカー (ポートからの入力を)**](ib--iw--id--input-from-port-.md)

 

 







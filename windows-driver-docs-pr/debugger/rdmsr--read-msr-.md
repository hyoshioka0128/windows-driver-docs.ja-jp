---
title: rdmsr (MSR の読み取り)
description: Rdmsr コマンドは、指定したアドレスからのモデルに固有の登録 (MSR) 値を読み取ります。
ms.assetid: 693f1be5-f215-4719-ae6f-30e367cefd77
keywords:
- rdmsr (読み取り MSR) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rdmsr (Read MSR)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be90d702d97c5eedd5b47254d33d873610264ca4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358550"
---
# <a name="rdmsr-read-msr"></a>rdmsr (MSR の読み取り)


**Rdmsr**コマンドを読み取り、[モデルに固有の登録 (MSR)](other-data-spaces.md)指定したアドレスからの値。

```dbgcmd
rdmsr Address 
```

## <a name="span-idddkcmdreadmsrdbgspanspan-idddkcmdreadmsrdbgspanparameters"></a><span id="ddk_cmd_read_msr_dbg"></span><span id="DDK_CMD_READ_MSR_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
MSR のアドレスを指定します。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**Rdmsr**コマンドは、x86、Itanium ベースおよび x64 ベースのプラットフォームで MSR を表示できます。 MSR 定義は、プラットフォーム固有です。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**wrmsr (MSR 書き込み)**](wrmsr--write-msr-.md)

 

 







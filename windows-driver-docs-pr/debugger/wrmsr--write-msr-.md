---
title: wrmsr (MSR の書き込み)
description: Wrmsr コマンドは、値をモデルに固有の登録 (MSR)、指定したアドレスを書き込みます。
ms.assetid: fe90b984-e2d6-4af7-b708-56fbcd2bbadd
keywords:
- wrmsr (書き込み MSR) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wrmsr (Write MSR)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b8391757e58bd6941cd717b6c446229cd6d147e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572026"
---
# <a name="wrmsr-write-msr"></a>wrmsr (MSR の書き込み)


**Wrmsr**コマンドは、値をモデルに固有の登録 (MSR)、指定したアドレスを書き込みます。

`wrmsr Address Value`

## <a name="span-idddkcmdwritemsrdbgspanspan-idddkcmdwritemsrdbgspanparameters"></a><span id="ddk_cmd_write_msr_dbg"></span><span id="DDK_CMD_WRITE_MSR_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
MSR のアドレスを指定します。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *値*   
MSR に書き込む 64 ビットの 16 進値を指定します。

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

 

<a name="remarks"></a>コメント
-------

**Wrmsr**コマンドは、x86、Itanium ベースおよび x64 ベースのプラットフォームで MSR を表示できます。 MSR 定義は、プラットフォーム固有です。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**rdmsr (読み取り MSR)**](rdmsr--read-msr-.md)

 

 







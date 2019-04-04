---
title: ur (x86 BIOS の逆アセンブル)
description: Ux のコマンドは、x86 ベースの BIOS コードの命令セットを表示します。
ms.assetid: d3616255-1a07-4a5d-8171-c8316179a7dc
keywords:
- ux (Unassemble x86 BIOS) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ux (Unassemble x86 BIOS)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b75f50578d869c83b2a5b22357d4a1ed41c477b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581178"
---
# <a name="ux-unassemble-x86-bios"></a>ur (x86 BIOS の逆アセンブル)


**Ux**コマンドは、x86 ベースの BIOS コードの命令セットを表示します。

`ux [Address]`

## <a name="span-idddkcmdunassemblex86biosdbgspanspan-idddkcmdunassemblex86biosdbgspanparameters"></a><span id="ddk_cmd_unassemble_x86_bios_dbg"></span><span id="DDK_CMD_UNASSEMBLE_X86_BIOS_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
X86 ベースの BIOS コード内のメモリのオフセットを指定します。 このパラメーターを省略するか、0 を指定すると場合、既定のオフセットは、BIOS の先頭にします。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

BIOS のコードをデバッグする方法の詳細については、[BIOS コードのデバッグ](debugging-bios-code.md)を参照してください。

<a name="remarks"></a>コメント
-------

デバッガーで表示から開始する手順については、最初の 8 行のコードから生成される、*アドレス*オフセット。

させる、 **ux**コマンド作業正しく、HAL シンボルできる必要があります、デバッガーにします。 デバッガーでは、これらのシンボルを見つけられない場合、デバッガーには、「解決できませんでした」エラーが表示されます。

 

 






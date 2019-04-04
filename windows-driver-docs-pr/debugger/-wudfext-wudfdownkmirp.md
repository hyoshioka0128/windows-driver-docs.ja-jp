---
title: wudfext.wudfdownkmirp
description: Wudfext.downkmmirp 拡張機能では、指定されたユーザー モードの I/O 要求パケット (IRP UM) に対応するカーネル モード I/O 要求パケット (IRP) を表示します。
ms.assetid: f5c42040-2349-4469-a398-12a238ff170e
keywords:
- デバッグ wudfext.wudfdownkmirp Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdownkmirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b5ff320dbf704fd8440d8ca943556bc84fdcc4be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559070"
---
# <a name="wudfextwudfdownkmirp"></a>!wudfext.wudfdownkmirp


**! Wudfext.downkmmirp**拡張機能は、指定されたユーザー モードの I/O 要求パケット (IRP UM) に対応するカーネル モード I/O 要求パケット (IRP) を表示します。

```dbgcmd
!wudfext.wudfdownkmirp Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
対応するカーネル モード IRP が表示される UM IRP のアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

使用することができます、 [ **! wudfext.umirps** ](-wudfext-umirps.md)ホスト プロセスですべて未処理 UM Irp の一覧を表示する拡張機能コマンド。

 

 






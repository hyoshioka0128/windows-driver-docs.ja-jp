---
title: mapped_file
description: Mapped_file 拡張機能では、指定したアドレスを含むファイルのマッピングをバックアップするファイルの名前が表示されます。
ms.assetid: 1d6d4d14-01ca-47ce-a044-778c9a56e9a5
keywords:
- Windows デバッグ mapped_file
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- mapped_file
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8a38e66b023c84fa72123bcd6d1f88908f8fc461
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336112"
---
# <a name="mappedfile"></a>! マップ\_ファイル


**! マップ\_ファイル**拡張機能は、指定したアドレスを含むファイルのマッピングをバックアップするファイルの名前を表示します。

```dbgcmd
!mapped_file Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ファイル マップのアドレスを指定します。 場合*アドレス*はマッピングでは、コマンドが失敗します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

**! マップ\_ファイル**拡張機能は、リモート オブジェクト以外のデバッグ中にのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ファイルのマッピングの詳細については、次を参照してください。 [MapViewOfFile](https://go.microsoft.com/fwlink/p/?linkid=123354) Windows SDK に含まれています。

<a name="remarks"></a>注釈
-------

ここでは、次の 3 つの例です。 使用される最初の 2 つのアドレスは、ファイルからマップされ、3 つ目はありません。

```dbgcmd
0:000> !mapped_file 4121ec 
Mapped file name for 004121ec: '\Device\HarddiskVolume2\CODE\TimeTest\Debug\TimeTest.exe'

0:000> !mapped_file 77150000 
Mapped file name for 77150000: '\Device\HarddiskVolume2\Windows\System32\kernel32.dll'

0:000> !mapped_file 80310000 
No information found for 80310000: error 87
```

 

 






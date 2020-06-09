---
title: mapped_file
description: Mapped_file 拡張機能には、指定されたアドレスを含むファイルマッピングをバックアップするファイルの名前が表示されます。
ms.assetid: 1d6d4d14-01ca-47ce-a044-778c9a56e9a5
keywords:
- Windows デバッグの mapped_file
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- mapped_file
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9d1591b541135a81dd416fe5746ead376baeb81b
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534933"
---
# <a name="mapped_file"></a>! マップされた \_ ファイル


**! マップ \_ ファイル**拡張子は、指定されたアドレスを含むファイルマッピングをバックアップするファイルの名前を表示します。

```dbgcmd
!mapped_file Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
ファイルマッピングのアドレスを指定します。 *アドレス*がマッピングに含まれていない場合、コマンドは失敗します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Uext .dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Uext .dll</p></td>
</tr>
</tbody>
</table>

 

! マップされた** \_ ファイル**の拡張子は、ライブの非リモートデバッグ中にのみ使用できます。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ファイルマッピングの詳細については、Windows SDK の「 [MapViewOfFile](https://docs.microsoft.com/windows/win32/api/memoryapi/nf-memoryapi-mapviewoffile) 」を参照してください。

<a name="remarks"></a>注釈
-------

次に3つの例を示します。 使用される最初の2つのアドレスはファイルからマップされ、3番目のアドレスはファイルから割り当てられません。

```dbgcmd
0:000> !mapped_file 4121ec 
Mapped file name for 004121ec: '\Device\HarddiskVolume2\CODE\TimeTest\Debug\TimeTest.exe'

0:000> !mapped_file 77150000 
Mapped file name for 77150000: '\Device\HarddiskVolume2\Windows\System32\kernel32.dll'

0:000> !mapped_file 80310000 
No information found for 80310000: error 87
```

 

 






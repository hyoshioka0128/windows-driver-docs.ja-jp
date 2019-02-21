---
title: storagekd.storlogsrb
description: Storagekd.storlogsrb 拡張機能は、ストレージ (または SCSI) のフィルター選択されたアダプターの Storport の内部のログ エントリを表示します。 要求ブロック (SRB) 提供します。
ms.assetid: 9E742636-DD19-4D8D-BDA1-C9BB8C293D8C
keywords:
- デバッグ storagekd.storlogsrb Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storlogsrb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ce1d0a0624552e02bc9231615a02d4925848b8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528299"
---
# <a name="storagekdstorlogsrb"></a>!storagekd.storlogsrb


**! Storagekd.storlogsrb**拡張機能は、ストレージ (または SCSI) のフィルター選択されたアダプターの Storport の内部のログ エントリを表示します。 要求ブロック (SRB) 提供します。

```dbgcmd
!storagekd.storlogsrb <Address> <srb> [<starting_entry> [<ending_entry>]] [L <count>]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
Storport アダプター デバイス拡張機能またはデバイス オブジェクトのアドレスを指定します。

<span id="_______SRB______"></span><span id="_______srb______"></span> *SRB*   
検索する SRB します。

<span id="_______starting_entry______"></span><span id="_______STARTING_ENTRY______"></span> *starting\_entry*   
先頭のエントリを表示する範囲。 指定しない場合、最後の*カウント*エントリが表示されます。

<span id="_______ending_entry______"></span><span id="_______ENDING_ENTRY______"></span> *ending\_entry*   
表示する範囲の終了エントリ。 指定しない場合、*カウント*以降で指定された項目では、項目が表示されます*開始\_エントリ*します。

<span id="_______count______"></span><span id="_______COUNT______"></span> *count*   
表示されるエントリの数。 指定しない場合、値 50 が使用されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 以降</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

 

 






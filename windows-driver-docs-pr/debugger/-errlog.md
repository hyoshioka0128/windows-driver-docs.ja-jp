---
title: curr.errlog と
description: Curr.errlog と拡張機能は、i/o システムのエラーログに保留中のエントリの内容を表示します。
ms.assetid: 2ef6331e-fa83-4515-8d70-5094e40b8497
keywords:
- curr.errlog と Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- errlog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 15ee478076f0db2fa073f31464ace6e1c5cbd9f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826762"
---
# <a name="errlog"></a>!errlog


**! Errlog**拡張機能は、i/o システムのエラーログに保留中のエントリの内容を表示します。

```dbgcmd
!errlog 
```

## <span id="ddk__errlog_dbg"></span><span id="DDK__ERRLOG_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

[**Iowriteerrorlogentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)の詳細については、Windows Driver KIT (WDK) のドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

このコマンドは、i/o システムのエラーログに記録されている保留中のイベントに関する情報を表示します。 これらは、 [**Iowriteerrorlogentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)関数の呼び出しによってキューに登録されたイベントで、後で**イベントビューアー**で表示するためにシステムのイベントログに書き込まれます。

[**Iowriteerrorlogentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)によってキューに登録されているが、エラーログにはコミットされていないエントリのみが表示されます。

このコマンドは、システムがクラッシュした後の診断支援として使用できます。これは、システムが停止する前にエラーログにコミットできなかった保留中のエラー情報を明らかにするためです。

 

 






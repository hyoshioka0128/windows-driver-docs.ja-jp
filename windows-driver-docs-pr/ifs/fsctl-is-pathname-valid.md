---
title: FSCTL_IS_PATHNAME_VALID 制御コード
description: FSCTL\_IS\_PATHNAME\_有効なコントロール コード指定されたパス名の静的分析を実行し、(たとえば、無効な文字がない、パス名の形式が適切かどうかを示すステータス値を返します許容されるパスの長さ、およびなど)。
ms.assetid: 3f95ae2c-a376-4c68-9e84-dde22aa7e315
keywords:
- FSCTL_IS_PATHNAME_VALID 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_IS_PATHNAME_VALID
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe0bd9f33aab2e45be2b17230cc9da9e03ebe1a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324602"
---
# <a name="fsctlispathnamevalid-control-code"></a>FSCTL\_IS\_PATHNAME\_有効なコントロール コード


**FSCTL\_IS\_PATHNAME\_有効**制御コードが指定されたパス名の静的分析を実行し、パス名が (たとえば、形式が適切かどうかを示すステータス値を返しますない無効な文字、許容される path 長、およびなど)。 「偽陽性です」提供場合がありますので、この分析は、ボリュームの内容が考慮されません。 つまり、分析は、パス名が整形式、それがない場合でも可能性があります。 負の値の結果より信頼性が高くが正しいとは限りません。

この制御コードは、高速 FAT ファイル システムでサポートされていませんし、NTFS または UDF で意味のある操作ではありません。 NTFS および UDF は、このようなさまざまコードセットを任意の文字列が有効なパス名では可能性のあるをサポートします。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 使用されていません。

<a href="" id="filehandle"></a>*FileHandle*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 使用されていません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 FSCTL を使用して、\_IS\_PATHNAME\_この操作に対して有効です。

<a href="" id="inputbuffer"></a>*InputBuffer*  
確認するパス名を NULL で終わる文字列を格納するバッファー。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
パス名の長さ、(バイト単位)。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
使用されていません。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
使用されていません。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_パス名の形式が適切である場合は成功します。 それ以外の場合、使用されるルーチンは、適切な NTSTATUS エラー コードを返します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

 

 






---
title: FSCTL_IS_PATHNAME_VALID 制御コード
description: FSCTL\_は\_PATHNAME\_有効なコントロールコードが指定されたパス名の静的分析を実行し、パス名が正しい形式であるかどうかを示す状態値を返します (たとえば、無効な文字、許容されるパス長、など)。
ms.assetid: 3f95ae2c-a376-4c68-9e84-dde22aa7e315
keywords:
- FSCTL_IS_PATHNAME_VALID 制御コードのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 77f44b6cc8c90b69bcd1b2f3b2ff80b561bc1a77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841296"
---
# <a name="fsctl_is_pathname_valid-control-code"></a>FSCTL\_は、有効なコントロールコード\_\_パス名です


**FSCTL\_は\_pathname\_有効な**コントロールコードが指定されたパス名の静的分析を実行し、パス名が正しい形式であるかどうかを示す状態値を返します (たとえば、無効な文字、許容されるパスは使用できません)。長さなど)。 この分析ではボリュームのコンテンツは考慮されないため、"偽陽性" が示されることがあります。 つまり、パス名が適切な形式であることが分析によって示されている可能性があります。 負の結果はより信頼性が高くなりますが、正確であるとは限りません。

この制御コードは、高速な FAT ファイルシステムではサポートされていません。 NTFS や UDF では意味のある操作ではありません。 NTFS および UDF では、このような広範なコードによって、任意の文字列が有効なパス名であることがサポートされています。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**パラメーター**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 使用されません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 使用されません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 FSCTL を使用する\_は、この操作に対して有効なパス名\_\_ます。

<a href="" id="inputbuffer"></a>*InputBuffer*  
確認する NULL で終わるパス名文字列を含むバッファー。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
パス名の長さ (バイト単位)。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
使用されません。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
使用されません。

<a name="status-block"></a>状態ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、パス名が正しい形式である場合、STATUS\_SUCCESS を返します。 それ以外の場合、使用されるルーチンは適切な NTSTATUS エラーコードを返します。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

 

 






---
title: FSCTL_LMR_GET_LINK_TRACKING_INFORMATION 制御コード
description: FSCTL\_LMR\_GET\_LINK\_は、\_情報制御コードは、ファイルのリンク追跡情報を取得します。
ms.assetid: 8ddb8aca-4998-47ed-b8c9-39219e342c2c
keywords:
- FSCTL_LMR_GET_LINK_TRACKING_INFORMATION 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_LMR_GET_LINK_TRACKING_INFORMATION
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f5451dd1a4cfffc11370eda7365599b3e24fee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841288"
---
# <a name="fsctl_lmr_get_link_tracking_information-control-code"></a>FSCTL\_LMR\_\_リンクを取得する\_\_情報制御コードを追跡する


**FSCTL\_LMR\_GET\_link\_は、\_情報**制御コードは、ファイルのリンク追跡情報を取得します。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 リモートボリュームのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 リモートボリュームのハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作の **\_情報を追跡\_には、FSCTL\_LMR\_** 使用して\_リンクを取得します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
なし。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
使用しません。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
ファイルのリンク追跡情報を格納している\_情報の構造を**追跡\_リンク**。

``` syntax
typedef struct _LINK_TRACKING_INFORMATION {
  LINK_TRACKING_INFORMATION_TYPE  Type;
  UCHAR  VolumeId[16];
} LINK_TRACKING_INFORMATION, *PLINK_TRACKING_INFORMATION;
```

<a href="" id="type"></a>**各種**  
ファイルが格納されているファイルシステムの種類を指定する **\_情報\_型**情報の列挙値を追跡\_リンク。 このメンバーが**Dfs Linktrackinginformation**の値を保持している場合、ファイルは分散ファイルシステム上に存在します。 このメンバーが**NtfsLinkTrackingInformation**の値を保持している場合、ファイルは NTFS ファイルシステム上に存在します。

<a href="" id="volumeid"></a>**VolumeId**  
ボリューム識別子を保持する符号なし文字配列。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*Outputbuffer*パラメーターが指すバッファーのサイズ (バイト単位)。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合、適切な関数は、適切な NTSTATUS エラーコードを返します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
</tbody>
</table>

 

 






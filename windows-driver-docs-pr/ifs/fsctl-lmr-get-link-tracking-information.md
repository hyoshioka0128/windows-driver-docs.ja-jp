---
title: FSCTL_LMR_GET_LINK_TRACKING_INFORMATION 制御コード
description: FSCTL\_LMR\_取得\_リンク\_追跡\_情報コントロール コード ファイルの追跡情報のリンクを取得します。
ms.assetid: 8ddb8aca-4998-47ed-b8c9-39219e342c2c
keywords:
- FSCTL_LMR_GET_LINK_TRACKING_INFORMATION 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 882bf7ac134d64d967caade3d99ca591c227aed2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380135"
---
# <a name="fsctllmrgetlinktrackinginformation-control-code"></a>FSCTL\_LMR\_取得\_リンク\_追跡\_情報制御コード


**FSCTL\_LMR\_取得\_リンク\_追跡\_情報**コントロール コード ファイルの追跡情報のリンクを取得します。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 リモート ボリュームのファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 リモート ボリュームのハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 使用**FSCTL\_LMR\_取得\_リンク\_追跡\_情報**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
なし。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
使用されていません。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
A**リンク\_追跡\_情報**ファイルの情報を追跡するリンクを含む構造体。

``` syntax
typedef struct _LINK_TRACKING_INFORMATION {
  LINK_TRACKING_INFORMATION_TYPE  Type;
  UCHAR  VolumeId[16];
} LINK_TRACKING_INFORMATION, *PLINK_TRACKING_INFORMATION;
```

<a href="" id="type"></a>**型**  
A**リンク\_追跡\_情報\_型**列挙値の情報に、ファイルが置かれているファイル システムの種類を指定します。 このメンバーの値を保持している場合**DfsLinkTrackingInformation**、分散ファイル システムにファイルが存在します。 このメンバーの値を保持している場合**NtfsLinkTrackingInformation**、NTFS ファイル システムにファイルが存在します。

<a href="" id="volumeid"></a>**VolumeId**  
ボリュームの識別子を保持する符号なし文字配列。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
指し示されるバッファーのバイト単位で、サイズ、 *OutputBuffer*パラメーター。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数は、適切な NTSTATUS エラー コードを返します。

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
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

 

 






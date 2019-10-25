---
title: FSCTL_MARK_VOLUME_DIRTY 制御コード
description: FSCTL\_MARK\_ボリューム\_ダーティコントロールコードは、指定されたボリュームをダーティとしてマークします。これにより、次のシステムの再起動時に Autochk.exe がボリューム上で実行されます。
ms.assetid: 9062b212-fc8a-4467-b32f-047fc3702445
keywords:
- FSCTL_MARK_VOLUME_DIRTY 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_MARK_VOLUME_DIRTY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7e7788529834de6336cf49c88f095f958913efd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841284"
---
# <a name="fsctl_mark_volume_dirty-control-code"></a>FSCTL\_マーク\_ボリューム\_ダーティコントロールコード


**FSCTL\_MARK\_ボリューム\_ダーティ**コントロールコードは、指定されたボリュームをダーティとしてマークします。これにより、次のシステムの再起動時に autochk.exe がボリューム上で実行されます。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="instance"></a>*Instance*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 FSCTL 要求を開始するミニフィルタードライバーインスタンスへの非透過インスタンスポインター。

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 ダーティとマークするボリュームを指定するファイルポインターオブジェクト。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 ダーティとマークされるボリュームへのハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作では、FSCTL\_使用して **\_ボリューム\_ダーティとマーク**します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。 を**NULL**に設定します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作では使用されません。 を0に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。 を**NULL**に設定します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。 を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)ルーチンは、STATUS\_SUCCESS または適切な NTSTATUS 値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p><em>FileObject</em>または<em>FileHandle</em>が有効なボリュームハンドルを表していないか、別のパラメーターが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>呼び出し元には、SE_MANAGE_VOLUME アクセス権がありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>ファイルシステムボリュームがマウント解除されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_TOO_LATE</strong></p></td>
<td align="left"><p>ファイルシステムボリュームがシャットダウンされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_MEDIA_WRITE_PROTECTED</strong></p></td>
<td align="left"><p>ファイルシステムボリュームは読み取り専用です。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**ReFS:  **このコードはサポートされていません。

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
<td align="left">Ntifs (FltKernel .h または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FSCTL\_が\_ボリューム\_ダーティ**](fsctl-is-volume-dirty.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 







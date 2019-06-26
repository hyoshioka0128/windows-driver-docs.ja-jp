---
title: FSCTL_MARK_VOLUME_DIRTY 制御コード
description: FSCTL\_マーク\_ボリューム\_ダーティ制御コードが、次のシステムの再起動中に、ボリューム上で実行する Autochk.exe をトリガーする、ダーティとして指定されたボリュームをマークします。
ms.assetid: 9062b212-fc8a-4467-b32f-047fc3702445
keywords:
- FSCTL_MARK_VOLUME_DIRTY 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 5ec703816f5154a7cae2ff48a5d794b779aa5462
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380113"
---
# <a name="fsctlmarkvolumedirty-control-code"></a>FSCTL\_マーク\_ボリューム\_ダーティ制御コード


**FSCTL\_マーク\_ボリューム\_DIRTY**制御コードが、次のシステムの再起動中に、ボリューム上で実行する Autochk.exe をトリガーする、ダーティとして指定されたボリュームをマークします。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance"></a>*インスタンス*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 不透明なインスタンスへのポインターを FSCTL 要求を開始するミニフィルター ドライバーのインスタンス。

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 ダーティとしてマークするボリュームを指定するファイル ポインター オブジェクト。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 ダーティとマークするのには、ボリュームへのハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作のコードを制御します。 使用**FSCTL\_マーク\_ボリューム\_DIRTY**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作で使用できません。 設定**NULL**します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作で使用できません。 0 に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作で使用できません。 設定**NULL**します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作で使用できません。 0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ルーチンがステータスを返します\_成功、または、適切な NTSTATUS値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p><em>FileObject</em>または<em>FileHandle</em>は有効なを表しませんボリューム ハンドルまたは別のパラメーターが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>呼び出し元には、SE_MANAGE_VOLUME アクセス権はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>ファイル システム ボリュームがマウント解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_TOO_LATE</strong></p></td>
<td align="left"><p>ファイル システム ボリュームをシャット ダウンします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_MEDIA_WRITE_PROTECTED</strong></p></td>
<td align="left"><p>ファイル システム ボリュームとは、読み取り専用です。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**ReFS:  **このコードはサポートされていません。

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
<td align="left">Ntifs.h (FltKernel.h または Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FSCTL\_IS\_ボリューム\_DIRTY**](fsctl-is-volume-dirty.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 







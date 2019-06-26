---
title: FSCTL_GET_EXTERNAL_BACKING 制御コード
description: FSCTL\_取得\_外部\_バッキング制御コードは、バッキング外部プロバイダーからファイルのバックアップ情報を取得します。
ms.assetid: 18A8E71E-CAED-4E0A-95D0-18E99F9733B2
keywords:
- FSCTL_GET_EXTERNAL_BACKING 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_GET_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 642e9f9c7f7ca848fe1a93390db59efaee4871a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365033"
---
# <a name="fsctlgetexternalbacking-control-code"></a>FSCTL\_取得\_外部\_バッキング制御コード


**FSCTL\_取得\_外部\_バックアップ**制御コードは、バッキング外部プロバイダーからファイルのバックアップ情報を取得します。 バッキング プロバイダーには、Windows Image Format (WIM) プロバイダーまたは個々 の圧縮ファイルのプロバイダーが含まれます。 外部からバックアップされたファイルのコンテンツを以外のクエリ対象のファイルを含む、ボリューム上のボリューム上に存在します。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 呼び出し元の非透過インスタンス ポインター。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 バックアップ情報の照会対象のファイルのファイル ポインター オブジェクト。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 バックアップ情報の照会対象のファイルのハンドル。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_取得\_外部\_バックアップ**この操作にします。

<a href="" id="inputbuffer--in-"></a>*InputBuffer\[で\]*  
なし。 設定**NULL**します。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
0 に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
受信するのに十分な大きさのサイズを持つ必要がある出力バッファーへのポインターを[ **WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wof_external_info)構造体のプロバイダー データが続きます。 WIM のバックアップ ファイル、 **WOF\_外部\_情報**が続く、 [ **WIM\_プロバイダー\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wim_provider_external_info)構造体。 個別に圧縮されたファイルの**WOF\_外部\_情報**が続く、 [**ファイル\_プロバイダー\_外部\_情報\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_provider_external_info_v1)構造体。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[アウト\]*  
指し示されるバッファーのバイト単位のサイズ*OutputBuffer*します。

<a href="" id="lengthreturned"></a>*LengthReturned*  
書き込まれたバイト数を指定します*OutputBuffer*が正常に完了します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数では NTSTATUS 値は次のいずれかを返す可能性があります。

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
<td align="left"><p><strong>STATUS_OBJECT_NOT_EXTERNALLY_BACKED</strong></p></td>
<td align="left"><p>ファイルは外部でバックアップされません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バックアップ サービスが存在しないか開始されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

更新するデータ ソースのバックアップ プロバイダーが、WIM ファイルの場合は、出力バッファーには、 [ **WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wof_external_info)構造が続く、 [**WIM\_プロバイダー\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wim_provider_external_info)構造体。 *OutputBufferLength*以上である必要があります**sizeof**(WOF\_外部\_情報) + **sizeof**(WIM\_プロバイダー\_外部\_情報)。 バックアップ プロバイダーが、個別に圧縮されたファイルの場合は、出力バッファーに格納されます、 **WOF\_外部\_情報**構造が続く、 [**ファイル\_プロバイダー\_外部\_情報\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_provider_external_info_v1)構造体。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8.1 Update 以降を利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_設定\_外部\_バックアップ**](fsctl-set-external-backing.md)

[**WIM\_プロバイダー\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wim_provider_external_info)

[**WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wof_external_info)

 

 







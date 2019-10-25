---
title: FSCTL_QUERY_PERSISTENT_VOLUME_STATE 制御コード
description: FSCTL\_クエリ\_永続的\_ボリューム\_状態制御コードは、ファイルシステムボリュームの永続的な設定を取得します。
ms.assetid: e54a03bb-9329-4095-bb81-857b46fee31c
keywords:
- FSCTL_QUERY_PERSISTENT_VOLUME_STATE 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_QUERY_PERSISTENT_VOLUME_STATE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 484e45c52465c5cf908ecd6ea0ae23adb88380e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841271"
---
# <a name="fsctl_query_persistent_volume_state-control-code"></a>FSCTL\_クエリ\_永続\_ボリューム\_状態制御コード


**FSCTL\_クエリ\_永続的\_ボリューム\_状態**制御コードは、ファイルシステムボリュームの永続的な設定を取得します。 永続設定は、コンピューターの再起動の間にファイルシステムボリュームに保持されます。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 ファイルシステムボリュームのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 ファイルシステムボリュームのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作には、 **FSCTL\_クエリ\_永続的\_ボリューム\_状態**を使用してください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
\_\_FS によって割り当てられたファイルへのポインターは、[**永続\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)の構造を保持します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*パラメーターが指すバッファーのサイズ (バイト単位)。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
\_\_FS によって割り当てられたファイルへのポインターは、ファイルシステムボリュームの永続的な設定を受け取る[**永続的な\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)構造を保持します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*Outputbuffer*パラメーターが指すバッファーのサイズ (バイト単位)。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、次のいずれかのような状態\_SUCCESS または適切な NTSTATUS 値を返します。

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
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>呼び出し元が、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"><strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>の<strong>version</strong>メンバーで正しくないバージョン番号を指定しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>ファイルシステムボリュームがオープンユーザーボリュームではないか、呼び出し元が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"><strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>の<strong>flagmask</strong>メンバーに無効なフラグを指定しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>InputBuffer</em>パラメーターが指すバッファーが十分な大きさではありません (つまり、バッファーが<strong>sizeof</strong>(FILE_FS_PERSISTENT_VOLUME_INFORMATION) 未満)。 この場合、永続的な設定データは返されません。 これはエラーコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>呼び出し元がファイルシステムボリュームにアクセスできません。</p></td>
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

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_FS\_永続的な\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_persistent_volume_information)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 







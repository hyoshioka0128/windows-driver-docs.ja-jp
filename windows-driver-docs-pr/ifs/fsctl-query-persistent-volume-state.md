---
title: FSCTL_QUERY_PERSISTENT_VOLUME_STATE 制御コード
description: FSCTL\_クエリ\_持続\_ボリューム\_状態制御コードをファイル システム ボリュームの永続的な設定を取得します。
ms.assetid: e54a03bb-9329-4095-bb81-857b46fee31c
keywords:
- FSCTL_QUERY_PERSISTENT_VOLUME_STATE 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 76e8cbeb4bd6709e8f028c3953d9afa77c66d768
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380096"
---
# <a name="fsctlquerypersistentvolumestate-control-code"></a>FSCTL\_クエリ\_持続\_ボリューム\_状態制御コード


**FSCTL\_クエリ\_持続\_ボリューム\_状態**制御コードをファイル システム ボリュームの永続的な設定を取得します。 永続的な設定は、コンピューターの再起動の間でファイル システム ボリューム上に残ります。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 ファイル システム ボリュームのファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 ファイル システム ボリュームのファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 使用**FSCTL\_クエリ\_持続\_ボリューム\_状態**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
呼び出し元が割り当てたへのポインター [**ファイル\_FS\_持続\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_persistent_volume_information)構造体。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
指し示されるバッファーのバイト単位で、サイズ、 *InputBuffer*パラメーター。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
呼び出し元が割り当てたへのポインター [**ファイル\_FS\_持続\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_persistent_volume_information)永続的な設定を受信する構造体ファイル システム ボリューム。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
指し示されるバッファーのバイト単位で、サイズ、 *OutputBuffer*パラメーター。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_成功、または、次のいずれかなどの適切な NTSTATUS 値。

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
<td align="left"><p>指定された呼び出しは不適切なバージョン番号を<strong>バージョン</strong>のメンバー <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"> <strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>ファイル システム ボリュームが、開いているユーザー ボリュームか、呼び出し元で無効なフラグを指定する、 <strong>FlagMask</strong>のメンバー <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_persistent_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_persistent_volume_information)"> <strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>バッファーを<em>InputBuffer</em>パラメーターが指してが十分な大きさでない (つまり、バッファーがより小さい<strong>sizeof</strong>(FILE_FS_PERSISTENT_VOLUME_INFORMATION))。 この場合、永続的な設定のデータは返されません。 これは、エラー コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>呼び出し元がファイル システム ボリュームにアクセスできません。</p></td>
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
<td align="left"><p>ファイル システム ボリュームは読み取り専用です。</p></td>
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
<td align="left"><p>Windows 7 以降で利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_FS\_持続\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_persistent_volume_information)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 







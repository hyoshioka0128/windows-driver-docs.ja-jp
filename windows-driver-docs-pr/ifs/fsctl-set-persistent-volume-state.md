---
title: FSCTL_SET_PERSISTENT_VOLUME_STATE 制御コード
description: FSCTL\_設定\_持続\_ボリューム\_状態制御コードは、ファイル システム ボリュームの永続的な設定を設定します。 永続的な設定は、コンピューターの再起動の間でファイル システム ボリューム上に残ります。
ms.assetid: 1670f3e9-c2f4-4696-a76e-bcf1bad5dc43
keywords:
- FSCTL_SET_PERSISTENT_VOLUME_STATE 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_SET_PERSISTENT_VOLUME_STATE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 697dd8aa46e2f1f83a51f4fb2b59b5d4d14ca875
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361921"
---
# <a name="fsctlsetpersistentvolumestate-control-code"></a>FSCTL\_設定\_持続\_ボリューム\_状態制御コード


**FSCTL\_設定\_持続\_ボリューム\_状態**制御コードは、ファイル システム ボリュームの永続的な設定を設定します。 永続的な設定は、コンピューターの再起動の間でファイル システム ボリューム上に残ります。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 ファイル システム ボリュームのファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 ファイル システム ボリュームのファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 使用**FSCTL\_設定\_持続\_ボリューム\_状態**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
呼び出し元が割り当てたへのポインター [**ファイル\_FS\_持続\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540280)永続的な設定を含む構造体ファイル システム ボリューム。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
指し示されるバッファーのバイト単位で、サイズ、 *InputBuffer*パラメーター。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。設定**NULL**します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_成功、または、次のいずれかなどの適切な NTSTATUS 値。

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
<td align="left"><p>要求されたレジストリの設定が 1 つのボリューム、または正しくないバージョン番号を指定した、<strong>バージョン</strong>のメンバー <a href="https://msdn.microsoft.com/library/windows/hardware/ff540280" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540280)"> <strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong> </a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>ファイル システム ボリュームが、開いているユーザー ボリュームか、呼び出し元で無効なフラグを指定する、 <strong>FlagMask</strong>のメンバー <a href="https://msdn.microsoft.com/library/windows/hardware/ff540280" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540280)"> <strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>バッファーを<em>InputBuffer</em>パラメーターが指してが永続的な設定のデータを保持するのに十分な大きさでないです。 この場合、永続的な設定のデータが設定されていません。 これは、エラー コードです。</p></td>
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


[**ファイル\_FS\_持続\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540280)

[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 







---
title: FSCTL_DELETE_EXTERNAL_BACKING 制御コード
description: FSCTL\_削除\_外部\_バッキング制御コードは、Windows Image Format (WIM) プロバイダー、圧縮ファイル プロバイダーなど、外部のバッキング プロバイダーとファイルの関連付けを削除します。
ms.assetid: 5C150899-6BCA-49EB-AEEB-0CBEC7BE60BA
keywords:
- FSCTL_DELETE_EXTERNAL_BACKING 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_DELETE_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ed30e496cbffc0a55f84fb574ef43cd12de7d2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582289"
---
# <a name="fsctldeleteexternalbacking-control-code"></a>FSCTL\_削除\_外部\_バッキング制御コード


**FSCTL\_削除\_外部\_バックアップ**制御コードは、外部のバッキング プロバイダー、Windows Image Format (WIM) プロバイダーを含むか、圧縮とファイルの関連付けを削除します。ファイルのプロバイダー。 、この操作の結果としてバックアップ ファイルの内容全体が読み取り、圧縮解除、およびファイルに書き込まれます。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 呼び出し元の非透過インスタンス ポインター。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 アソシエーションのバックアップを削除するファイルのファイル ポインター オブジェクト。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 アソシエーションのバックアップを削除するファイルのハンドル。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_削除\_外部\_バックアップ**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
なし。 NULL に設定します。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
0 に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
なし。 NULL に設定します。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[アウト\]*  
0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数では NTSTATUS 値は次のいずれかを返す可能性があります。

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
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>要求元には、ファイルのバックアップの関連付けを削除するアクセス許可がありません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

削除操作の結果としては、ファイルの内容がバックアップ ソースから読み取られ、ファイル全体がボリュームに書き込まれます。

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


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_設定\_外部\_バックアップ**](fsctl-set-external-backing.md)

 

 







---
title: FSCTL_ENUM_OVERLAY 制御コード
description: FSCTL\_ENUM\_オーバーレイ コントロールのコードは、指定されたボリュームのバックアップ プロバイダーからのすべてのデータ ソースを列挙します。
ms.assetid: 146A7D77-034F-4C06-99B8-8EBA6E7F0A40
keywords:
- FSCTL_ENUM_OVERLAY 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_ENUM_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37404a1e47e980836fc981c080ec2b376f4f3bfc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327880"
---
# <a name="fsctlenumoverlay-control-code"></a>FSCTL\_ENUM\_オーバーレイ コントロール コード


**FSCTL\_ENUM\_オーバーレイ**制御コードは、指定されたボリュームのバックアップ プロバイダーからのすべてのデータ ソースを列挙します。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 呼び出し元のポインターを不透明なインスタンス。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 マウントを解除するボリュームを指定する、ファイル ポインター オブジェクト。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 マウントを解除するボリュームのファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作のコードを制御します。 使用**FSCTL\_削除\_オーバーレイ**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
含める必要がありますが、入力バッファーへのポインターを[ **WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)構造体。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
設定**sizeof**(WOF\_外部\_情報)。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
1 つまたは複数を受信する出力バッファーへのポインター [ **WIM\_プロバイダー\_オーバーレイ\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/dn632451)ボリュームをバックアップするデータ ソースの構造体。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[アウト\]*  
バッファーのサイズが指す*OutputBuffer*、(バイト単位)。

<a href="" id="lengthreturned--out-"></a>*LengthReturned\[アウト\]*  
書き込まれたバイト数を指定します*OutputBuffer*が正常に完了します。

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
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>リクエスターでは、管理者特権はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>によって示される出力バッファーの長さ<em>OutputBuffer</em>とで指定した<em>OutputBufferLength</em>が小さすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>要求されたボリュームにアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バックアップ サービスが存在しないか開始されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

出力バッファーの配列には WIM プロバイダーのデータ ソースを列挙するときに[ **WIM\_プロバイダー\_オーバーレイ\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/dn632451)構造体。 出力バッファーのサイズは、オーバーレイのすべてのエントリを格納するのに十分な大きさである必要がありますまたは呼び出しの状態が返す\_バッファー\_すぎます\_小さい。

追加のバックアップ プロバイダーでは、特定の列挙の構造を定義します。

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

[**FSCTL\_追加\_オーバーレイ**](fsctl-add-overlay.md)

[**WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)

 

 







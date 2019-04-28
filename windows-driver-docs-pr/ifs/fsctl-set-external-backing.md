---
title: FSCTL_SET_EXTERNAL_BACKING 制御コード
description: FSCTL\_設定\_外部\_バッキング制御コードは Windows Image Format (WIM) ファイルまたは外部バックアップ プロバイダーによって、圧縮されたファイルなど、ファイルのバックアップ ソースを設定します。
ms.assetid: 5CB9FD4D-AF29-4438-B0B5-49871102968A
keywords:
- FSCTL_SET_EXTERNAL_BACKING 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_SET_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac3fa1240ceee4ed55cc212cc929e5aba22acc7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361932"
---
# <a name="fsctlsetexternalbacking-control-code"></a>FSCTL\_設定\_外部\_バッキング制御コード


**FSCTL\_設定\_外部\_バックアップ**制御コードは、Windows Image Format (WIM) ファイルまたは外部バックアップ プロバイダーによって、圧縮されたファイルなど、ファイルのバックアップ ソースを設定します。 以外のファイルが存在するボリューム上のボリュームは、外部からバックアップされたファイルのコンテンツをソースとする可能性があります。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 呼び出し元の非透過インスタンス ポインター。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 バックアップを設定する対象のファイルのファイル ポインター オブジェクト。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 バックアップを設定する対象のファイルのハンドル。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_設定\_外部\_バックアップ**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
含まれていますが、入力バッファーへのポインター [ **WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)構造体のプロバイダー データが続きます。 WIM のバックアップ ファイル、 **WOF\_外部\_情報**が続く、 [ **WIM\_プロバイダー\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632448)構造体。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
提供されるデータのサイズ、 *InputBuffer*します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
なし。 NULL に設定します。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength\[で\]*  
0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な NTSTATUS 値が返されます。

<a name="remarks"></a>注釈
-------

追加されたデータ ソースのバックアップ プロバイダーが WIM プロバイダーの場合は、入力バッファーに格納されます、 [ **WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)構造が続く、 [**WIM\_プロバイダー\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632448)構造体。 *InputBufferLength*ここでは、 **sizeof**(**WOF\_外部\_情報**) + **sizeof**(**WIM\_プロバイダー\_外部\_情報**)。

個別に圧縮されたファイルは変更されません、実行可能ファイルを含むデータの適切な圧縮を提供します。 書き込み用にこれらが開いて、ファイルが透過的に圧縮されていない状態になります。 入力バッファーには個別に圧縮されたファイルを指定するには、および、 [ **WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)構造が続く、 [**ファイル\_プロバイダー\_外部\_情報\_V1** ](https://msdn.microsoft.com/library/windows/hardware/mt426732)構造体。 *InputBufferLength*ここでは、 **sizeof**(**WOF\_外部\_情報**) + **sizeof**(**ファイル\_プロバイダー\_外部\_情報\_V1**)。 個々 の圧縮されたファイルでは、Windows 10 以降で使用できます。

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

[**FSCTL\_削除\_外部\_バックアップ**](fsctl-delete-external-backing.md)

[**FSCTL\_取得\_外部\_バックアップ**](fsctl-get-external-backing.md)

[**WIM\_プロバイダー\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632448)

[**WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)

 

 







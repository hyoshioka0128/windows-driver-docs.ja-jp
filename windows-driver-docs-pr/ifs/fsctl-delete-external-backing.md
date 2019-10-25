---
title: FSCTL_DELETE_EXTERNAL_BACKING 制御コード
description: FSCTL\_DELETE\_外部\_バッキングコントロールコードは、ファイルと外部バッキングプロバイダー (Windows イメージフォーマット (WIM) プロバイダーや圧縮ファイルプロバイダーなど) との関連付けを解除します。
ms.assetid: 5C150899-6BCA-49EB-AEEB-0CBEC7BE60BA
keywords:
- FSCTL_DELETE_EXTERNAL_BACKING 制御コードのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 6a2072c3a3efd9ecf93f418a4e49bfc2caee5956
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841325"
---
# <a name="fsctl_delete_external_backing-control-code"></a>FSCTL\_\_外部\_バッキングコントロールコードの削除


**FSCTL\_DELETE\_外部\_バッキング**コントロールコードは、ファイルと外部バッキングプロバイダー (Windows イメージフォーマット (WIM) プロバイダーや圧縮ファイルプロバイダーなど) との関連付けを解除します。 この操作の結果として、バックアップされたファイルの内容全体が読み取り、圧縮解除され、ファイルに書き込まれます。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="instance--in-"></a> *\]のインスタンス \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 バッキングアソシエーションが削除されるファイルのファイルポインターオブジェクト。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 バッキングアソシエーションが削除されたファイルのハンドル。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作を行うには、FSCTL\_使用して**外部\_\_削除**します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
なし。 を NULL に設定します。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
を0に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
なし。 を NULL に設定します。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合、適切な関数は、次のいずれかの NTSTATUS 値を返す可能性があります。

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
<td align="left"><p><strong>STATUS_OBJECT_NOT_EXTERNALLY_BACKED</strong></p></td>
<td align="left"><p>ファイルが外部でサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バッキングサービスが存在しないか、開始されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>要求元には、ファイルのバッキングアソシエーションを削除するアクセス許可がありません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

削除操作の結果として、ファイルの内容がバッキングソースから読み取られ、ファイル全体がボリュームに書き込まれます。

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
<td align="left"><p>Windows 8.1 更新プログラムから使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**外部\_バッキング\_FSCTL\_設定**](fsctl-set-external-backing.md)

 

 







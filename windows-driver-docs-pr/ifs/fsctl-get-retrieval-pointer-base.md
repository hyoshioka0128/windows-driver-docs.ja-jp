---
title: FSCTL_GET_RETRIEVAL_POINTER_BASE 制御コード
description: FSCTL\_GET\_取得\_ポインター\_BASE は、ボリュームの先頭に対して相対的なファイルシステムの最初の論理クラスター番号 (LCN) にセクターオフセットを返します。
ms.assetid: 2c342e58-ef9a-487a-beb9-4353dcbc8115
keywords:
- FSCTL_GET_RETRIEVAL_POINTER_BASE 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_GET_RETRIEVAL_POINTER_BASE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 884431651cc443633e5cfd39cd8eb5c9573669ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841304"
---
# <a name="fsctl_get_retrieval_pointer_base-control-code"></a>FSCTL\_取得\_取得\_ポインター\_基本コントロールコード


**FSCTL\_GET\_取得\_ポインター\_BASE**は、ボリュームの先頭に対して相対的なファイルシステムの最初の論理クラスター番号 (LCN) にセクターオフセットを返します。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)関数または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)関数を呼び出します。

**パラメーター**

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 ベースを取得するために、 **FSCTL\_GET\_retrieve\_\_ポインター**によって取得されるボリュームのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 ベースを取得するために、 **FSCTL\_GET\_retrieve\_\_ポインター**によって取得されるボリュームのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

\_ボリューム\_名前のアクセス権を管理\_には、このハンドルを SE で開く必要があります。 詳細については、「[ファイルセキュリティとアクセス権](https://docs.microsoft.com/windows/desktop/FileIO/file-security-and-access-rights)」を参照してください。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作では、FSCTL\_使用して **\_取得\_ポインター\_ベースを取得**します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。 を**NULL**に設定します。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
この操作では使用されません。 を0に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
ボリュームの先頭を基準とした、ファイルシステムの最初の LCN へのセクターオフセットを受け取る、大きな\_整数へのポインター。

<a href="" id="outputbufferlength--in-"></a> *\]の OutputBufferLength \[*  
出力バッファーのサイズ (バイト単位)。 この値は8である必要があります。

<a name="status-block"></a>状態ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、次のいずれかのような状態\_SUCCESS または適切な NTSTATUS 値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">期間</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>操作は成功しました。 OutputBuffer には、ボリュームの開始位置を基準とした、ファイルシステムの最初の LCN に対するセクターオフセットが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>ユーザーには、SE_MANAGE_VOLUME アクセス権がありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>OutputBuffer は、結果に対して十分な大きさではありません。 バッファーに情報が書き込まれていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>パラメーターが有効ではありませんでした。たとえば、使用されるハンドルが有効なボリュームハンドルではありません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

FSCTL によって取得された値を追加すると、FSCTL\_GET\_\_によって取得された値に基づいて取得された\_取得\_\_ポインターによって取得されます。\_は、ボリューム相対ファイルエクステントオフセットが生成されます。

FastFAT と exFAT デバイスでは、FSCTL\_GET\_取得\_ポインター\_基本制御コードを使用できます。 この機能は、フラッシュドライブなどのデバイスでの BitLocker の使用をサポートしています。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Server 2008 R2、Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ntifs</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 







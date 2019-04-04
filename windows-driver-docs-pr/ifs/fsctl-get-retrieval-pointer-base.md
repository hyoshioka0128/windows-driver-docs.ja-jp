---
title: FSCTL_GET_RETRIEVAL_POINTER_BASE 制御コード
description: FSCTL\_取得\_取得\_ポインター\_ベースは、ボリュームの先頭からの相対ファイル システムの最初の論理クラスター番号 (LCN) にセクター オフセットを返します。
ms.assetid: 2c342e58-ef9a-487a-beb9-4353dcbc8115
keywords:
- FSCTL_GET_RETRIEVAL_POINTER_BASE 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 5e74d5378ac92f6698bcbd0e96be9b2305e33e39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553322"
---
# <a name="fsctlgetretrievalpointerbase-control-code"></a>FSCTL\_取得\_取得\_ポインター\_基本コントロールのコード


**FSCTL\_取得\_取得\_ポインター\_ベース**ボリュームの先頭からの相対ファイル システムの最初の論理クラスター番号 (LCN) に、セクター オフセットを返します。

この操作を実行するには、呼び出し、 [ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)関数または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)を次の関数パラメーター。

**パラメーター**

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 対象のボリュームのファイル オブジェクト ポインター **FSCTL\_取得\_取得\_ポインター\_基本**ベースを取得することです。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 対象のボリュームのファイル ハンドル**FSCTL\_取得\_取得\_ポインター\_基本**ベースを取得することです。 このパラメーターが必要とすることはできません**NULL**します。

Se、このハンドルを開く必要がある\_管理\_ボリューム\_アクセス権の名前。 詳細については、[ファイルのセキュリティとアクセス権](https://msdn.microsoft.com/library/windows/desktop/aa364399)を参照してください。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_取得\_取得\_ポインター\_ベース**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作で使用できません。 設定**NULL**します。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
この操作で使用できません。 0 に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
大きなへのポインター\_整数で、ボリュームの先頭からの相対ファイル システムの最初の lcn セクター オフセットを受け取ります。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength\[で\]*  
(バイト単位)、出力バッファーのサイズ。 この値は、8 を指定する必要があります。

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
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>操作が正常に完了しました。 OutputBuffer には、ボリュームの先頭からの相対ファイル システムの最初の lcn セクター オフセットが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>ユーザーには、SE_MANAGE_VOLUME アクセスはありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>OutputBuffer が結果十分な大きさではありません。 バッファーに情報が書き込まれたありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>パラメーターが無効です。たとえば、使用されるハンドルは、有効なボリュームのハンドルではありません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

FSCTL によって取得された値を追加する\_取得\_取得\_ポインター\_FSCTL によって取得された値にベース\_取得\_取得\_ポインターは、コードの結果を制御ボリュームの相対ファイル エクステントのオフセット。

FSCTL\_取得\_取得\_ポインター\_FastFAT および exFAT のデバイスで、基本コントロールのコードを使用できます。 この機能は、フラッシュ ドライブなどのデバイス用の BitLocker の使用をサポートします。

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
<td align="left"><p>Windows Server 2008 R2、Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 







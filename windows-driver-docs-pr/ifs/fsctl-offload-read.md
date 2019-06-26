---
title: FSCTL_OFFLOAD_READ 制御コード
description: FSCTL\_オフロード\_読み取り制御コードのオフロードをサポートするストレージ システム内のデータのブロックがプリミティブを読み取る、オフロード読み取りを開始します。
ms.assetid: D9A22A8F-9B7E-4BF7-8FBD-267BE4C8DC59
keywords:
- FSCTL_OFFLOAD_READ 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_OFFLOAD_READ
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a05f79788ff75ca58f23cb86c3fafb2170dd832
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380116"
---
# <a name="fsctloffloadread-control-code"></a>FSCTL\_オフロード\_読み取り制御コード


**FSCTL\_オフロード\_読み取り**のオフロードをサポートするストレージ システム内のデータのブロックがプリミティブを読み取るコードはコントロールが、オフロード読み取りを開始します。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 呼び出し元の非透過インスタンス ポインター。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 ファイルからの読み取りを示すファイル ポインター オブジェクト。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 読み取るファイルのファイル ハンドル。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_オフロード\_読み取り**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
ポインターを[ **FSCTL\_オフロード\_読み取り\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_input)構造体は、読み取るデータ ブロックのオフセットとサイズが含まれています。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
指し示されるバッファーのバイト単位のサイズを*InputBuffer*します。 この値は**sizeof**(FSCTL\_オフロード\_読み取り\_入力)。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
ポインターを[ **FSCTL\_オフロード\_読み取り\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_output)オフロードの結果を受け取る構造体は、読み取り操作。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[アウト\]*  
指し示されるバッファーのバイト単位で、サイズ、 *OutputBuffer*パラメーター。 この値は以上である必要があります**sizeof**(FSCTL\_オフロード\_読み取り\_出力)。

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
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>指定されたハンドルは、有効なファイル ハンドルではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>ファイル サイズは、PAGE_SIZE 未満です。</p>
<p>\- または -</p>
<p><em>InputBufferLength</em> &lt; <strong>sizeof</strong>(FSCTL_OFFLOAD_READ_INPUT)。</p>
<p>\- または -</p>
<p>1 つ以上のこれらのメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_input)"> <strong>FSCTL_OFFLOAD_READ_INPUT</strong> </a>が正しくありません。</p>
<strong>FileOffset</strong>ボリュームの論理セクター サイズの倍数ではありません。
<strong>CopyLength</strong>ボリュームの論理セクター サイズの倍数ではありません。
<strong>サイズ</strong>が、サイズ、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_input)"> <strong>FSCTL_OFFLOAD_READ_INPUT</strong> </a>構造体。
<strong>FileOffset</strong> + <strong>CopyLength</strong> &gt; <strong>MAXULONGLONG</strong>します。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>ファイル システム ボリュームがマウント解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>操作は、このボリュームでサポートされていない読み取りの負荷を軽減します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OFFLOAD_READ_FILE_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>要求されたファイルの種類がサポートされていません。 オフロード操作は、これらのファイルの種類にはサポートされません。</p>
<ul>
<li>トランザクション ファイル (TxF)</li>
<li>非ユーザー ファイル</li>
<li>圧縮されたファイル</li>
<li>暗号化されたファイル</li>
<li>スパース ファイル</li>
<li>NTFS メタデータ ファイル</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_FILE_DELETED</strong></p></td>
<td align="left"><p>このファイルのデータ ストリームが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_CLOSED</strong></p></td>
<td align="left"><p>ファイル ハンドルは閉じられます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_HANDLE</strong></p></td>
<td align="left"><p>指定したファイル ハンドルが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_LOCK_CONFLICT</strong></p></td>
<td align="left"><p>現在のためが不足している読み取りアクセスはファイル ロック状態です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p><strong>FileOffset</strong>のメンバー <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_input)"> <strong>FSCTL_OFFLOAD_READ_INPUT</strong> </a>ファイル終端 (EOF) した後に開始します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_DISMOUNTED_VOLUME</strong></p></td>
<td align="left"><p>マウント解除されたボリューム上の読み取り、オフロードは発生しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOUCES</strong></p></td>
<td align="left"><p>リソース不足、要求を完了に利用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBufferLength</em>に対して小さすぎる<em>OutputBuffer</em>を受信する、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_output" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_OUTPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_output)"> <strong>FSCTL_OFFLOAD_READ_OUTPUT</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

読み取るオフロードでは、通常のファイルにのみ使用できます。 説明を参照して**状態\_オフロード\_読み取り\_ファイル\_いない\_サポートされている**サポートされていないファイルの種類の一覧についてはします。

読み取りが有効なデータの長さ (VDL) を超えるが EOF を超えないようにを開始することができます。

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
<td align="left"><p>Windows 8 以降で利用できます。</p></td>
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

[**FSCTL\_オフロード\_読み取り\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_input)

[**FSCTL\_オフロード\_読み取り\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_output)

 

 







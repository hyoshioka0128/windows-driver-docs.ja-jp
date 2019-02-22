---
title: FSCTL_OFFLOAD_WRITE 制御コード
description: FSCTL\_オフロード\_書き込み制御コードは記憶域システムをサポートしていますが書き込みプリミティブをオフロードすることで、オフロード書き込みデータのブロックを開始します。
ms.assetid: A40C6D4C-D31D-423E-B7B0-51151EEDD30F
keywords:
- FSCTL_OFFLOAD_WRITE 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_OFFLOAD_WRITE
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7573505f1b1cbc3a273cf623afa3d41dd769d170
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560528"
---
# <a name="fsctloffloadwrite-control-code"></a>FSCTL\_オフロード\_コントロール コードの記述


**FSCTL\_オフロード\_書き込み**制御コードは記憶域システムをサポートしていますが書き込みプリミティブをオフロードすることで、オフロード書き込みデータのブロックを開始します。

ミニフィルター ドライバーの呼び出しは、この操作を実行する[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)の次のパラメーターとファイル システム リダイレクター、および従来のファイル システム フィルター ドライバー呼び出し[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**パラメーター**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 呼び出し元の非透過インスタンス ポインター。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 書き込み先のファイルを指定するファイルのポインター オブジェクト。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 書き込み先のファイルのファイル ハンドル。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_オフロード\_書き込み**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
ポインターを[ **FSCTL\_オフロード\_書き込み\_入力**](https://msdn.microsoft.com/library/windows/hardware/hh451126)構造体は、読み取るデータ ブロックのオフセットとサイズが含まれています。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
指し示されるバッファーのバイト単位のサイズを*InputBuffer*します。 この値は**sizeof**(FSCTL\_オフロード\_書き込み\_入力)。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
ポインターを[ **FSCTL\_オフロード\_書き込み\_入力**](https://msdn.microsoft.com/library/windows/hardware/hh451126)構造体は、読み取るデータ ブロックのオフセットとサイズが含まれています。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[アウト\]*  
指し示されるバッファーのバイト単位で、サイズ、 *OutputBuffer*パラメーター。 この値は以上である必要があります**sizeof**(FSCTL\_オフロード\_読み取り\_出力)。

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
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>指定されたハンドルは、有効なファイル ハンドルではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>ファイル サイズは、PAGE_SIZE 未満です。</p>
<p>- または -</p>
<p><em>InputBufferLength</em> &lt; <strong>sizeof</strong>(FSCTL_OFFLOAD_WRITE_INPUT)。</p>
<p>- または -</p>
<p>1 つ以上のこれらのメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451126" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451126)"> <strong>FSCTL_OFFLOAD_WRITE_INPUT</strong> </a>が正しくありません。</p>
<strong>FileOffset</strong>ボリュームの論理セクター サイズの倍数ではありません。
<strong>CopyLength</strong>ボリュームの論理セクター サイズの倍数ではありません。
<strong>TransferOffset</strong>ボリュームの論理セクター サイズの倍数ではありません。
<strong>サイズ</strong>が、サイズ、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451126" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451126)"> <strong>FSCTL_OFFLOAD_WRITE_INPUT</strong> </a>構造体。
<strong>FileOffset</strong> &gt;ファイルの有効なデータの長さ (VDL)。
<strong>FileOffset</strong> + <strong>CopyLength</strong> &gt; <strong>MAXULONGLONG</strong>します。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>操作は、このボリュームでサポートされていない読み取りの負荷を軽減します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_OFFLOAD_WRITE_FILE_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>要求されたファイルの種類がサポートされていません。 オフロード操作は、これらのファイルの種類にはサポートされません。</p>
<ul>
<li>トランザクション ファイル (TxF)</li>
<li>非ユーザー ファイル</li>
<li>圧縮されたファイル</li>
<li>スパース ファイル</li>
<li>暗号化されたファイル</li>
<li>NTFS メタデータ ファイル</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_TOO_LATE</strong></p></td>
<td align="left"><p>書き込み操作は、マウント解除した後に、ボリュームにしようとしました。</p></td>
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
<td align="left"><p>現在のファイルがロック状態のため、読み取りまたは書き込みアクセス権を付与できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p><strong>FileOffset</strong>のメンバー <a href="https://msdn.microsoft.com/library/windows/hardware/hh451126" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451126)"> <strong>FSCTL_OFFLOAD_WRITE_INPUT</strong> </a>ファイル終端 (EOF) した後に開始します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_DISMOUNTED_VOLUME</strong></p></td>
<td align="left"><p>オフロードの書き込みは、マウント解除されたボリュームで発生することはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_MEDIA_WRITE_PROTECTED</strong></p></td>
<td align="left"><p>ボリュームが読み取り専用です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOUCES</strong></p></td>
<td align="left"><p>リソース不足、要求を完了に利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>InputBufferLength</em>に対して小さすぎる<em>InputBuffer</em>を格納する、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451126" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451126)"> <strong>FSCTL_OFFLOAD_WRITE_INPUT</strong> </a>構造体。</p>
<p>- または -</p>
<p><em>OutputBufferLength</em>に対して小さすぎる<em>OutputBuffer</em>を受信する、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451130" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_OUTPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451130)"> <strong>FSCTL_OFFLOAD_WRITE_OUTPUT</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

読み取るオフロードでは、通常のファイルにのみ使用できます。 説明を参照して**状態\_オフロード\_書き込み\_ファイル\_いない\_サポートされている**サポートされていないファイルの種類の一覧についてはします。

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
<td align="left"><p>Windows 8 以降で利用できます。</p></td>
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

[**FSCTL\_オフロード\_書き込み\_入力**](https://msdn.microsoft.com/library/windows/hardware/hh451126)

[**FSCTL\_オフロード\_書き込み\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh451130)

 

 







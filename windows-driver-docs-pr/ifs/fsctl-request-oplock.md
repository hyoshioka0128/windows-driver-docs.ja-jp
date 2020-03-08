---
title: FSCTL_REQUEST_OPLOCK 制御コード
description: FSCTL\_要求\_OPLOCK 制御コードは、ファイルに対して便宜的ロック (oplock) を要求するか、oplock の解除が発生したことを確認します。
ms.assetid: a36f2a13-d450-4903-b999-6ba574ab3f6e
keywords:
- FSCTL_REQUEST_OPLOCK コントロールコードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_REQUEST_OPLOCK
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dd7c871d8eea9311ba3cfd5bcde9317a9d0084d
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910387"
---
# <a name="fsctl_request_oplock-control-code"></a>FSCTL\_要求\_OPLOCK 制御コード


**FSCTL\_要求\_oplock**制御コードは、ファイルに対して便宜的ロック (oplock) を要求するか、oplock の解除が発生したことを確認します。

便宜的ロックの詳細については、Windows デスクトップのドキュメントの「[便宜的ロック](https://docs.microsoft.com/windows/desktop/FileIO/opportunistic-locks)」を参照してください。 ユーザーモードの OPLOCK コントロールの詳細については、Windows デスクトップのドキュメントの「[ファイル管理制御コード](https://docs.microsoft.com/windows/desktop/FileIO/file-management-control-codes)」を参照してください。

この制御コードを処理するために、ファイルシステムまたはフィルタードライバーは、次のパラメーターを使用して[**FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)を呼び出します。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの不透明な oplock オブジェクトポインターです。

<a href="" id="irp"></a>*Irp*  
IRP\_MJ\_ファイル\_システム\_CONTROL FSCTL 要求の IRP へのポインター。 操作の*Fscontrolcode*パラメーターは、FSCTL\_要求\_OPLOCK である必要があります。

<a href="" id="opencount"></a>*OpenCount*  
要求が排他的な oplock の場合は、ファイルのユーザーハンドルの数。 要求が共有可能な oplock に対するものである場合、ファイルにバイト範囲ロックが存在しない場合、 *Opencount*は0になります。 それ以外の場合、 *Opencount*は0以外になります。 呼び出し元は、IRP で[**FsRtlOplockIsSharedRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockissharedrequest)ルーチンを呼び出して、要求が共有可能な oplock 用かどうかを判断できます。

<a href="" id="flags"></a>*示す*  
関連付けられた oplock 操作のビットマスク。 ファイルシステムまたはフィルタードライバーは、ビットを設定して[**FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)の動作を指定します。 *Flags*パラメーターには、次のオプションがあります。

<a href="" id="oplock-fsctrl-flag-all-keys-match--0x00000001-"></a>OPLOCK\_FSCTRL\_フラグ\_すべての\_\_キーに一致する (0x00000001)  
現在開いているハンドルですべての便宜的ロックキーが一致することをファイルシステムが検証したことを示します。 このフラグを指定することにより、oplock パッケージは、ファイルに対して複数の開いているハンドルが存在する場合に、レベル RW または RWH の oplock を与えることができます。 Oplock の種類の詳細については、「[概要](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-overview)」を参照してください。

<a name="status-block"></a>ステータス ブロック
------------

[**FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)は、この操作に対して次のいずれかの NTSTATUS 値を返します。

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
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>Oplock が付与されました。 これは成功コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_CANCELLED</strong></p></td>
<td align="left"><p>IRP は、FSCTL_REQUEST_OPLOCK 操作が完了する前に取り消されました。 これはエラーコードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OPLOCK_NOT_GRANTED</strong></p></td>
<td align="left"><p>Oplock を許可できませんでした。 これはエラーコードです。</p></td>
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
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>参照


[**FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)

[**FsRtlOplockIsSharedRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockissharedrequest)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 







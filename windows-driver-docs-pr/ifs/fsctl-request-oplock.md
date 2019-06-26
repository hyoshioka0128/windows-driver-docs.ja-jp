---
title: FSCTL_REQUEST_OPLOCK 制御コード
description: FSCTL\_要求\_OPLOCK 制御コードは、ファイルの便宜的ロック (oplock) を要求または oplock が発生したことを確認します。
ms.assetid: a36f2a13-d450-4903-b999-6ba574ab3f6e
keywords:
- FSCTL_REQUEST_OPLOCK 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 2f0a121a939b4d2cdb4661109aa5add4290e32d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380038"
---
# <a name="fsctlrequestoplock-control-code"></a>FSCTL\_要求\_OPLOCK 制御コード


**FSCTL\_要求\_OPLOCK**制御コードは、ファイルの便宜的ロック (oplock) を要求または oplock が発生したことを確認します。

便宜的ロックの詳細については、次を参照してください。[便宜的ロック](https://docs.microsoft.com/windows/desktop/FileIO/opportunistic-locks)、Windows デスクトップ ドキュメント。 ユーザー モードの OPLOCK のコントロールの詳細については、次を参照してください。[ファイル管理の制御コード](https://docs.microsoft.com/windows/desktop/FileIO/file-management-control-codes)、Windows デスクトップ ドキュメント。

ファイル システムまたはフィルター ドライバーを呼び出し、この制御コードを処理する[ **FsRtlOplockFsctrlEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)次のパラメーターを使用します。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの oplock の不透明なオブジェクトのポインター。

<a href="" id="irp"></a>*Irp*  
IRP の IRP へのポインター\_MJ\_ファイル\_システム\_コントロール FSCTL 要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_要求\_OPLOCK します。

<a href="" id="opencount"></a>*OpenCount*  
要求が排他の oplock の場合は、ファイルのハンドルをユーザーの数。 要求が共有できる、oplock の場合*オープン カウント*ファイルにバイト範囲ロックが存在しない場合は 0。 それ以外の場合、*オープン カウント*が 0 以外。 呼び出し元が呼び出すことができます、 [ **FsRtlOplockIsSharedRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockissharedrequest)要求が共有できる oplock のかどうかを判断する IRP のルーチンです。

<a href="" id="flags"></a>*フラグ*  
Oplock が関連する操作に対応するビットマスク。 ファイル システムまたはフィルター ドライバーの動作を指定するビットを設定する[ **FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)します。 *フラグ*パラメーターには、次のオプション。

<a href="" id="oplock-fsctrl-flag-all-keys-match--0x00000001-"></a>OPLOCK\_FSCTRL\_FLAG\_ALL\_KEYS\_MATCH (0x00000001)  
便宜的ロックのすべてのキーが現在開かれているいずれかのハンドルに一致するファイル システムが検証することを指定します。 このフラグを指定すると、oplock のパッケージをファイルに 1 つ以上の開いているハンドルが存在する場合のレベルの RW または RWH oplock を与えることができます。 Oplock の種類の詳細については、次を参照してください。[概要](https://docs.microsoft.com/windows-hardware/drivers/ifs/overview)します。

<a name="status-block"></a>ステータス ブロック
------------

[**FsRtlOplockFsctrlEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)この操作は次の NTSTATUS の値を返します。

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
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>Oplock が与えられました。 これは、成功コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_CANCELLED</strong></p></td>
<td align="left"><p>FSCTL_REQUEST_OPLOCK 操作が完了する前に、IRP が取り消されました。 これは、エラー コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OPLOCK_NOT_GRANTED</strong></p></td>
<td align="left"><p>Oplock を取得できませんでした。 これは、エラー コードです。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)

[**FsRtlOplockIsSharedRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockissharedrequest)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 







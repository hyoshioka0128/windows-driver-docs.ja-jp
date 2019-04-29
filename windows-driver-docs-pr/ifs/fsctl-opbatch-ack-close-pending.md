---
title: FSCTL_OPBATCH_ACK_CLOSE_PENDING 制御コード
description: FSCTL\_OPBATCH\_ACK\_閉じる\_保留中のコントロール、コードが通知に応答する (レベル 1、バッチ、またはフィルター)、排他ファイルの便宜的ロック (oplock) が切断されました。
ms.assetid: 310cd778-5a1c-46e2-8c05-127fc754ecfe
keywords:
- FSCTL_OPBATCH_ACK_CLOSE_PENDING 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_OPBATCH_ACK_CLOSE_PENDING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fe5dba53a67fcc37ac01a399e65fe113c1af10a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324556"
---
# <a name="fsctlopbatchackclosepending-control-code"></a>FSCTL\_OPBATCH\_ACK\_閉じる\_保留中の制御コード


**FSCTL\_OPBATCH\_ACK\_閉じる\_PENDING**制御コードは通知に応答する (レベル 1、バッチ、またはフィルター)、排他便宜的ロック (oplock) ファイルには切断されました。 クライアント アプリケーションでは、このコントロールのコードを oplock が受信確認し、ファイル ハンドルを終了しようとしていることを示すために送信します。

バッチまたはフィルターの oplock 区切りのため、呼び出し元は、この制御コードを送信した後、ファイル ハンドルを閉じる必要があります。 それ以外の場合、システムでは、ファイル ハンドルを閉じての待機がブロックされます。

この制御コードは、レベル 1 の各 oplock を処理するためのものではありません。 ただし、レベル 1 の oplock の中断の完了の確認として扱われますこの制御コードと、呼び出し元がファイル ハンドルを終了する必要はありません。

この制御コードはほとんど使用されません。 クライアント アプリケーションはファイルの場合、oplock の通知され、そのファイル ハンドルを閉じ、ときに、システムは、oplock の完全な受信確認として、ファイル ハンドルを閉じるを扱います。 そのためこの制御コードを送信する必要はありません。

ミニフィルターを呼び出し、この制御コードを処理する[ **FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)次のパラメーターを使用します。 ファイル システムまたはレガシ フィルター ドライバーを呼び出す[ **FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)します。

便宜的ロックおよび FSCTL についての詳細については\_OPBATCH\_ACK\_閉じる\_制御コード、保留中、Microsoft Windows SDK のマニュアルを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの oplock の不透明なオブジェクトのポインター。

<a href="" id="callbackdata"></a>*ここ*  
[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)のみです。 コールバック データ ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) IRP の構造\_MJ\_ファイル\_システム\_コントロール FSCTL要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_OPBATCH\_ACK\_閉じる\_保留します。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)のみです。 IRP の IRP\_MJ\_ファイル\_システム\_コントロール FSCTL 要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_OPBATCH\_ACK\_閉じる\_保留します。

<a href="" id="opencount"></a>*OpenCount*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398) FLT は常に返します\_PREOP\_この操作を完了します。

[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)この操作は次の NTSTATUS の値を返します。

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
<td align="left"><p>このハンドルによって保持されている oplock が分割されている処理中でした。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>このハンドルによって保持された oplock がないか、oplock は現在進行中のありません。 これは、エラー コードです。</p></td>
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


[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IRP のパラメーター\_MJ\_ファイル\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff543398)

[**FSCTL\_OPLOCK\_BREAK\_ACK\_NO\_2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL\_OPLOCK\_中断\_ACKNOWLEDGE**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_フィルター\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 







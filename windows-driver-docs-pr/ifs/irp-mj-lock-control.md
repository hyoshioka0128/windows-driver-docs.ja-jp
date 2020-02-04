---
title: IRP_MJ_LOCK_CONTROL
description: IRP\_MJ\_ロック\_コントロール
ms.assetid: db21d779-c423-42bd-a94b-4d8c8fd1f7cb
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_LOCK_CONTROL
topic_type:
- apiref
api_name:
- IRP_MJ_LOCK_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18f82f19c414c57f90247857dde941c5334f452f
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977669"
---
# <a name="irp_mj_lock_control"></a>IRP\_MJ\_ロック\_コントロール


## <a name="when-sent"></a>送信時


IRP\_MJ\_LOCK\_CONTROL 要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ターゲットデバイスオブジェクトがファイルシステムのコントロールデバイスオブジェクトであるかどうかを判断するために、ファイルオブジェクトを抽出してデコードする必要があります。 この場合、ファイルシステムドライバーは、ロック要求を処理せずに、必要に応じて IRP を完了する必要があります。

そうしないと、ユーザーファイルを開くハンドルに対して要求が発行された場合、ファイルシステムドライバーは、マイナー関数コードによって示された操作を実行し、IRP を完了する必要があります。 それ以外の場合、ドライバーは IRP を失敗させる必要があります。

有効なマイナー関数コードを次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_LOCK</p></td>
<td align="left"><p>Microsoft Win32 <strong>LockFile</strong>関数を呼び出したユーザーモードアプリケーションに代わって、バイト範囲ロック要求を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_UNLOCK_ALL</p></td>
<td align="left"><p>ファイルに対するすべてのバイト範囲ロックを解放する要求を示します。通常は、ファイルオブジェクトへの最後の未処理ハンドルが閉じられているためです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_UNLOCK_ALL_BY_KEY</p></td>
<td align="left"><p>指定されたキー値を持つすべてのバイト範囲ロックを解放する要求を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_UNLOCK_SINGLE</p></td>
<td align="left"><p>Microsoft Win32 <strong>UnlockFile</strong>関数を呼び出したユーザーモードアプリケーションに代わって、1つのバイト範囲ロックを解放する要求を示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


ファイルシステムフィルタードライバーは、必要な処理を実行した後、スタック上の次の下位のドライバーに IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、ロック制御要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ\_LOCK\_CONTROL の処理中は、ファイル\_オブジェクト構造の関連性の**あるフィールドは**無効であるため、使用できません。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  
次の1つまたは複数を実行します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_EXCLUSIVE_LOCK</p></td>
<td align="left"><p>このフラグが設定されている場合は、排他的なバイト範囲ロックが要求されます。 それ以外の場合は、共有ロックが要求されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_FAIL_IMMEDIATELY</p></td>
<td align="left"><p>このフラグが設定されている場合、ロック要求はすぐに許可されない場合は失敗します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP\_MJ\_ロック\_コントロールを指定します。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
次のいずれかを指定します。

-   IRP\_\_ロック
-   IRP\_\_ロック解除\_すべて
-   IRP\_、\_キーによってすべての\_\_ロック解除\_
-   IRP\_\_のロック解除\_SINGLE

<a href="" id="irpsp--parameters-lockcontrol-byteoffset"></a>*IrpSp-&gt;パラメーター。 LockControl. ByteOffset*  
ロックまたはロック解除するバイト範囲のファイル内の開始バイトオフセット。

<a href="" id="irpsp--parameters-lockcontrol-key"></a>*IrpSp-&gt;パラメーター。 LockControl。キー*  
バイト範囲ロックのキー。

<a href="" id="irpsp--parameters-lockcontrol-length"></a>*IrpSp-&gt;Parameters. LockControl. Length*  
ロックまたはロック解除するバイト範囲の長さ (バイト単位)。

## <a name="see-also"></a>「


[**FltProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

 

 







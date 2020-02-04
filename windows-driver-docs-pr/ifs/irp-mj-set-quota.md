---
title: IRP_MJ_SET_QUOTA
description: IRP\_MJ\_設定\_クォータ
ms.assetid: 256c349b-48cb-4a9f-a60a-89503d8f3f58
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_SET_QUOTA
topic_type:
- apiref
api_name:
- IRP_MJ_SET_QUOTA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eb937c51d15ef06b50b19bb22a86c9e684ed844
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977667"
---
# <a name="irp_mj_set_quota"></a>IRP\_MJ\_設定\_クォータ


## <a name="when-sent"></a>送信時


IRP\_MJ\_SET\_クォータ要求は、i/o マネージャーによって送信されます。 たとえば、ユーザーモードアプリケーションが**Idiskquotacontrol::** などの Microsoft Win32 メソッドを呼び出した場合に、これを送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


IRP\_MJ\_SET\_QUOTA および IRP\_MJ\_クエリ\_クォータは Windows NT 4.0 に存在しましたが、ファイルシステムでは使用されませんでした。 Windows 2000 以降のシステムでは、NTFS でディスククォータをサポートするために使用されます。 新しいファイルシステムによるこれらの Irp のサポートはオプションです。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、クォータの動作を明示的にオーバーライドする必要がない限り、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、set quota information 要求の処理で、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="deviceobject--flags"></a>*DeviceObject-&gt;フラグ*  
DO\_バッファリング\_IO フラグが設定されている場合、呼び出し元はバッファーされた i/o\_メソッドを要求しました。 それ以外の場合、呼び出し元は、i/o ではなく\_メソッドを要求しました。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
\_バッファー\_IO フラグが*DeviceObject-&gt;フラグ*で設定されている場合に、中間システムバッファーとして使用されるシステム指定のバッファーへのポインター。 それ以外の場合、このメンバーは**NULL**に設定されます。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
ボリュームに対して追加または変更するクォータエントリを格納する、呼び出し元が指定したバッファーへのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_\_MJ の処理中に、ファイル\_オブジェクト構造の "関連性のある" フィールドが無効になります。この**フィールドは、** クォータ\_クォータを設定して使用する必要があります。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
\_クォータを設定\_IRP\_MJ を指定します。

<a href="" id="irpsp--parameters-setquota-length"></a>*IrpSp-&gt;Parameters. SetQuota. Length*  
*Irp&gt;UserBuffer*が指すバッファーの長さをバイト単位で指定します。

## <a name="see-also"></a>「


[**ファイル\_クォータの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckQuotaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)

 

 







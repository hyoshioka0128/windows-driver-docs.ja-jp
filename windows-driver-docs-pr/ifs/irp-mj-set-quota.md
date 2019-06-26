---
title: IRP_MJ_SET_QUOTA
description: IRP\_MJ\_SET\_QUOTA
ms.assetid: 256c349b-48cb-4a9f-a60a-89503d8f3f58
keywords:
- IRP_MJ_SET_QUOTA インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_SET_QUOTA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aa5ab1ab0e9a7c5c1cc75c332210e701beb047f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359254"
---
# <a name="irpmjsetquota"></a>IRP\_MJ\_SET\_QUOTA


## <a name="when-sent"></a>送信時


IRP\_MJ\_設定\_クォータ要求が I/O マネージャーによって送信されます。 送信できる、たとえば、ユーザー モード アプリケーションには Microsoft Win32 メソッドが呼び出されるとなど**IDiskQuotaControl::SetQuotaState**します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


IRP\_MJ\_設定\_クォータと IRP\_MJ\_クエリ\_クォータは、Windows NT 4.0 に存在していましたが、ファイル システムで使用されていません。 Windows 2000 およびそれ以降のシステムでは、NTFS でディスク クォータのサポートのために使用されます。 新しいファイル システムでこれらの Irp のサポートは、省略可能です。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


クォータの動作を明示的にオーバーライドする必要がある場合を除き、フィルター ドライバー スタックで、次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のセットのクォータ情報の要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="deviceobject--flags"></a>*デバイス オブジェクト-&gt;フラグ*  
場合、操作を行います\_バッファーに格納された\_IO フラグが設定されて、呼び出し元のメソッドが要求した\_I/O のバッファーに格納します。 それ以外の場合、呼び出し元のメソッドが要求\_も I/O。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
システムが指定した場合に、中間システム バッファーとして使用するバッファーへのポインター、DO\_バッファーに格納された\_IO フラグに設定されて*デバイス オブジェクト -&gt;フラグ*。 このメンバーに設定している場合は、 **NULL**します。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
クォータ エントリを追加またはボリュームの変更を格納している呼び出し元が指定のバッファーへのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_設定\_クォータ使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_設定\_クォータ。

<a href="" id="irpsp--parameters-setquota-length"></a>*IrpSp-&gt;Parameters.SetQuota.Length*  
指し示されるバッファーのバイト単位の長さを指定します*Irp -&gt;UserBuffer*します。

## <a name="see-also"></a>関連項目


[**ファイル\_クォータ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_quota_information)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoCheckQuotaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)

 

 







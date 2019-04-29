---
title: IRP_MJ_QUERY_QUOTA
description: IRP\_MJ\_クエリ\_クォータ
ms.assetid: eb48b5ef-7eac-49d4-ab23-2d3efe783fa3
keywords:
- IRP_MJ_QUERY_QUOTA インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_QUOTA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e357c69101e8cec982202ee73c664ad2b4274b47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324324"
---
# <a name="irpmjqueryquota"></a>IRP\_MJ\_クエリ\_クォータ

## <a name="when-sent"></a>送信時

IRP\_MJ\_クエリ\_クォータ要求が I/O マネージャーによって送信されます。 この要求を送信できますなど、ユーザー モード アプリケーションには Microsoft Win32 メソッドが呼び出されるとなど**IDiskQuotaControl::GetQuotaState**します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー

ファイル システムでは、ディスク クォータをサポートする場合、ファイル システム ドライバーを抽出し、ファイルまたはディレクトリのユーザーのオープンを表すかどうかを確認するファイル オブジェクトをデコードします。 場合は、ドライバーは、クエリの処理し、IRP を完了する必要があります。 それ以外の場合、ドライバーでは、クエリを処理することがなく適切な IRP を完了する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー

クォータの動作を明示的にオーバーライドする必要がある場合を除き、フィルター ドライバー スタックで、次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター

ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP スタックの場所はクエリのクォータ情報の要求の処理には、次のメンバーで設定されている情報を使用できます。

### <a name="deviceobject"></a>*デバイス オブジェクト*  

ターゲット デバイスのオブジェクトへのポインター。

### <a name="deviceobject-flags"></a>*デバイス オブジェクトのフラグを -> します。*  

DO\_バッファーに格納された\_IO、および DO\_直接\_IO フラグを使用するデータは、ドライバーに渡される方法を指定する次のように。

|フラグの設定|I/O メソッド|
|----|----|
|~DO_BUFFERED_IO|~ DO_DIRECT_IO|
|METHOD_NEITHER|~DO_BUFFERED_IO|
|DO_DIRECT_IO|METHOD_DIRECT|
|DO_BUFFERED_IO|~ DO_DIRECT_IO|
|METHOD_BUFFERED|DO_BUFFERED_IO|
|DO_DIRECT_IO|METHOD_BUFFERED|

### <a name="irp-associatedirpsystembuffer"></a>*Irp AssociatedIrp.SystemBuffer を -> します。*

システムが指定した場合に、中間システム バッファーとして使用するバッファーへのポインター、DO\_バッファーに格納された\_IO フラグに設定されて*デバイス オブジェクトには、フラグが]-> [* します。 このメンバーに設定している場合は、 **NULL**します。

### <a name="irp-iostatus"></a>*Irp IoStatus を -> します。*

ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

### <a name="irp-userbuffer"></a>*Irp UserBuffer を -> します。*  

呼び出し元が指定したファイルへのポインター\_クォータ\_をボリュームのクォータ情報を受け取る情報構造の出力バッファー。

### <a name="irpsp-fileobject"></a>*IrpSp FileObject を -> します。*

関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp FileObject]-> [* パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_クエリ\_クォータ使用しないでください。

### <a name="irpsp-flags"></a>*IrpSp フラグを -> します。*

このメンバーには、次の 1 つ以上を指定できます。

|Flag|説明|
|----|----|
|SL_INDEX_SPECIFIED|クォータの一覧で指定するインデックスを持つエントリでスキャンを開始*IrpSp Parameters.QueryQuota.StartSid を ->*|
|SL_RESTART_SCAN|一覧の最初のエントリでスキャンを開始します。 このフラグが設定されていない場合は、前の IRP_MJ_QUERY_QUOTA 要求からのスキャンを再開します。|
|SL_RETURN_SINGLE_ENTRY|見つかった最初のエントリのみを返します。|

### <a name="irpsp-majorfunction"></a>*IrpSp MajorFunction を -> します。*

IRP を指定します\_MJ\_クエリ\_クォータ。

### <a name="irpsp-parametersqueryquotalength"></a>*IrpSp Parameters.QueryQuota.Length を -> します。*

指すバッファーの長さをバイト単位で*Irp UserBuffer]-> [* します。

### <a name="irpsp-parametersqueryquotasidlist"></a>*IrpSp Parameters.QueryQuota.SidList を -> します。*

クォータ情報が返される Sid の一覧への省略可能なポインター。 リスト内の各エントリは、 [**ファイル\_取得\_クォータ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540298)構造体。 この構造体の定義は次のとおりです。

```cpp
typedef struct _FILE_GET_QUOTA_INFORMATION {
    ULONG NextEntryOffset;
    ULONG SidLength;
    SID Sid;
} FILE_GET_QUOTA_INFORMATION, *PFILE_GET_QUOTA_INFORMATION;
```

|Member|説明|
|-----|----|
|NextEntryOffset|複数のエントリが、バッファーに存在する場合は [次へ] の FILE_GET_QUOTA_INFORMATION エントリのバイト オフセット。 この 1 つに後に他のエントリがない場合、このメンバーは 0 を使用します。|
|SidLength|(バイト単位) の長さの**Sid**メンバー。|
|sid|セキュリティ識別子 (SID)|

### <a name="irpsp-parametersqueryquotasidlistlength"></a>*IrpSp Parameters.QueryQuota.SidListLength を -> します。*

長さをバイト単位で指定されている場合、Sid の一覧。

#### <a name="irpsp-parametersqueryquotastartsid"></a>*IrpSp Parameters.QueryQuota.StartSid を -> します。*

返される情報は、先頭以外のエントリを開始することを示す SID への省略可能なポインター。 SID の一覧が指定されている場合、このパラメーターは無視されます。

## <a name="see-also"></a>関連項目

[**ファイル\_取得\_クォータ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_get_quota_information)

[**ファイル\_クォータ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_quota_information)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoCheckQuotaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_SET\_QUOTA**](irp-mj-set-quota.md)

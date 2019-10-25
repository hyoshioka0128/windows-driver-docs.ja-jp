---
title: IRP_MJ_QUERY_QUOTA
description: IRP\_MJ\_クエリ\_クォータ
ms.assetid: eb48b5ef-7eac-49d4-ab23-2d3efe783fa3
keywords:
- IRP_MJ_QUERY_QUOTA インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_QUOTA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59a72d3cc14faa756523c5872ba00bb89460bf08
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841164"
---
# <a name="irp_mj_query_quota"></a>IRP\_MJ\_クエリ\_クォータ

## <a name="when-sent"></a>送信時

IRP\_MJ\_クエリ\_クォータ要求は、i/o マネージャーによって送信されます。 この要求は、たとえば、ユーザーモードアプリケーションが**Idiskquotacontrol::** などの Microsoft Win32 メソッドを呼び出したときに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー

ファイルシステムがディスククォータをサポートしている場合、ファイルシステムドライバーはファイルオブジェクトを抽出してデコードし、ファイルまたはディレクトリが開いているユーザーを表すかどうかを判断します。 その場合、ドライバーはクエリを処理し、IRP を完了する必要があります。 それ以外の場合、ドライバーはクエリを処理せずに、必要に応じて IRP を完了する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー

フィルタードライバーは、クォータの動作を明示的にオーバーライドする必要がない限り、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター

ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、次の IRP のメンバーと、クエリクォータ情報要求の処理での IRP スタックの場所に設定されている情報を使用できます。

### <a name="deviceobject"></a>*DeviceObject*  

ターゲットデバイスオブジェクトへのポインター。

### <a name="deviceobject-flags"></a>*DeviceObject-> フラグ*  

次のようにして、データをドライバーに渡す方法を指定するために、IO\_IO フラグと\_DIRECT\_IO フラグを使用して\_します。

|フラグの設定|I/o メソッド|
|----|----|
|~ DO_BUFFERED_IO|~ DO_DIRECT_IO|
|METHOD_NEITHER|~ DO_BUFFERED_IO|
|DO_DIRECT_IO|METHOD_DIRECT|
|DO_BUFFERED_IO|~ DO_DIRECT_IO|
|METHOD_BUFFERED|DO_BUFFERED_IO|
|DO_DIRECT_IO|METHOD_BUFFERED|

### <a name="irp-associatedirpsystembuffer"></a>*Irp-> AssociatedIrp*

\_バッファー\_IO フラグが*DeviceObject-> フラグ*で設定されている場合に、中間システムバッファーとして使用されるシステム指定のバッファーへのポインター。 それ以外の場合、このメンバーは**NULL**に設定されます。

### <a name="irp-iostatus"></a>*Irp > IoStatus*

最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

### <a name="irp-userbuffer"></a>*Irp-> UserBuffer*  

呼び出し元から提供されたファイル\_クォータ\_情報を指すポインター。ボリュームのクォータ情報を受け取ります。

### <a name="irpsp-fileobject"></a>*IrpSp-> FileObject*

*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-> FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_obect 構造体でもあります。 IRP\_MJ\_QUERY\_のクォータの処理中に、ファイル\_オブジェクト構造の関連性の**あるフィールドは**無効です。使用しないでください。

### <a name="irpsp-flags"></a>*IrpSp-> フラグ*

このメンバーは、次の1つまたは複数にすることができます。

|Flag|意味|
|----|----|
|SL_INDEX_SPECIFIED|Irpsp-> パラメーターでインデックスが指定されているクォータリストのエントリで、スキャンを開始*します。 QueryQuota. StartSid*|
|SL_RESTART_SCAN|一覧の最初のエントリからスキャンを開始します。 このフラグが設定されていない場合は、以前の IRP_MJ_QUERY_QUOTA 要求からスキャンを再開します。|
|SL_RETURN_SINGLE_ENTRY|最初に見つかったエントリだけを返します。|

### <a name="irpsp-majorfunction"></a>*IrpSp-> MajorFunction*

IRP\_MJ\_クエリ\_クォータを指定します。

### <a name="irpsp-parametersqueryquotalength"></a>*IrpSp-> Parameters. QueryQuota. Length*

*Irp > UserBuffer*が指すバッファーの長さ (バイト単位)。

### <a name="irpsp-parametersqueryquotasidlist"></a>*IrpSp-> Parameters. QueryQuota. SidList*

クォータ情報が返される Sid のリストへのポインター (省略可能)。 リスト内の各エントリは、 [ **\_クォータ\_情報の構造を取得\_ファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_quota_information)です。 この構造体は次のように定義されています。

```cpp
typedef struct _FILE_GET_QUOTA_INFORMATION {
    ULONG NextEntryOffset;
    ULONG SidLength;
    SID Sid;
} FILE_GET_QUOTA_INFORMATION, *PFILE_GET_QUOTA_INFORMATION;
```

|メンバー|意味|
|-----|----|
|NextEntryOffset|バッファー内に複数のエントリが存在する場合は、次の FILE_GET_QUOTA_INFORMATION エントリのバイトオフセット。 このメンバーは、このメンバーの後に他のエントリがない場合は0になります。|
|SidLength|**Sid**メンバーの長さ (バイト単位)。|
|Sid|セキュリティ識別子 (SID)|

### <a name="irpsp-parametersqueryquotasidlistlength"></a>*IrpSp-> パラメーター。 QueryQuota. SidListLength*

Sid のリスト (指定されている場合) の長さ (バイト単位)。

#### <a name="irpsp-parametersqueryquotastartsid"></a>*IrpSp-> Parameters. QueryQuota. StartSid*

返された情報が最初のエントリ以外のエントリで開始されることを示す SID へのポインター (省略可能)。 SID リストが指定されている場合、このパラメーターは無視されます。

## <a name="see-also"></a>関連項目

[**ファイル\_\_クォータ\_情報の取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_quota_information)

[**ファイル\_クォータの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckQuotaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_設定\_クォータ**](irp-mj-set-quota.md)

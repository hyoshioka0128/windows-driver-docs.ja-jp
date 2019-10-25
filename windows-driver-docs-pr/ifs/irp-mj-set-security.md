---
title: IRP_MJ_SET_SECURITY
description: IRP\_MJ\_設定\_セキュリティ
ms.assetid: 8d8b06b9-5d63-4506-831c-9c533dbe95f4
keywords:
- IRP_MJ_SET_SECURITY インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_SET_SECURITY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cc86d366df014fdc6abe0e851a3175f70e14190
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841161"
---
# <a name="irp_mj_set_security"></a>IRP\_MJ\_設定\_セキュリティ


## <a name="when-sent"></a>送信時


IRP\_MJ\_SET\_セキュリティ要求は、i/o マネージャーによって送信されます。 この要求は、たとえば、ユーザーモードアプリケーションが**Setsecurityinfo**などの Win32 関数を呼び出したときに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ファイルオブジェクトを抽出してデコードし、ユーザーファイルまたはディレクトリが開いているかどうかを判断する必要があります。 その場合、ドライバーは要求を処理し、IRP を完了する必要があります。 それ以外の場合、ドライバーは要求を処理せずに、必要に応じて IRP を完了する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、set security information 要求の処理で、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最後の完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_obect 構造体でもあります。 IRP\_\_\_MJ の処理中に、ファイル\_オブジェクト構造**の "関連性**のある" フィールドは無効になります。セキュリティで保護されているため、使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
セキュリティ\_設定\_IRP\_MJ を指定します。

<a href="" id="irpsp--parameters-setsecurity-securitydescriptor"></a>*IrpSp-&gt;パラメーター。 SetSecurity. SecurityDescriptor*  
オブジェクトに割り当てるセキュリティ情報の値を格納している[**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))の構造体へのポインター。

<a href="" id="irpsp--parameters-setsecurity-securityinformation"></a>*IrpSp-&gt;パラメーター。 SetSecurity. SecurityInformation*  
セキュリティ記述子に設定するセキュリティ情報を指定する[**セキュリティ\_情報**](security-information.md)型の値。 この値には、次のいずれかを指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SecurityInformation の値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの随意アクセス制御リスト (DACL) が設定されていることを示します。 WRITE_DAC アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのプライマリグループ識別子が設定されていることを示します。 WRITE_OWNER アクセスが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの所有者識別子が設定されていることを示します。 WRITE_OWNER アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのシステム ACL (SACL) が設定されていることを示します。 ACCESS_SYSTEM_SECURITY アクセスが必要です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="see-also"></a>関連項目


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クエリ\_セキュリティ**](irp-mj-query-security.md)

[**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**セキュリティ\_情報**](security-information.md)

 

 







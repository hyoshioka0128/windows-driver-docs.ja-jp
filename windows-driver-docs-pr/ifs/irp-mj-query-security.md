---
title: IRP_MJ_QUERY_SECURITY
description: IRP\_MJ\_クエリ\_セキュリティ
ms.assetid: f0f73bfe-c016-49e2-b725-380f46a9b9d6
keywords:
- IRP_MJ_QUERY_SECURITY インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_SECURITY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5793729095fb4a95787e78ce6b78e894728a42f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841162"
---
# <a name="irp_mj_query_security"></a>IRP\_MJ\_クエリ\_セキュリティ


## <a name="when-sent"></a>送信時


IRP\_MJ\_QUERY\_セキュリティ要求は、i/o マネージャーによって送信されます。 たとえば、ユーザーモードアプリケーションが**Getsecurityinfo**などの Microsoft Win32 関数を呼び出した場合に、これを送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ファイルオブジェクトを抽出してデコードし、ユーザーファイルまたはディレクトリが開いているかどうかを判断する必要があります。 その場合、ドライバーはクエリを処理し、IRP を完了する必要があります。 それ以外の場合、ドライバーはクエリを処理せずに、必要に応じて IRP を完了する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、クエリセキュリティ要求の処理で、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最後の完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指定したオブジェクトのセキュリティ記述子のコピーを受け取る、呼び出し元から提供される出力バッファーへのポインター。 呼び出しプロセスには、オブジェクトのセキュリティステータスの指定した側面を表示する権限が必要です。 [**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))の構造体は、自己相対形式で返されます。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

Windows XP 以降では、ファイルオブジェクトは名前付きデータストリームを表すことができます。 名前付きデータストリームの詳細については、「[**ファイル\_ストリームの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)」を参照してください。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ\_クエリ\_セキュリティの処理中は、ファイル\_オブジェクト構造**の "関連性**のある" フィールドは無効です。このフィールドは使用できません。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP\_MJ\_クエリ\_セキュリティを指定します。

<a href="" id="irpsp--parameters-querysecurity-length"></a>*IrpSp-&gt;Parameters. QuerySecurity. Length*  
*Irp&gt;UserBuffer*パラメーターが指すバッファーのサイズ (バイト単位)。

<a href="" id="irpsp--parameters-querysecurity-securityinformation"></a>*IrpSp-&gt;パラメーター。 QuerySecurity. SecurityInformation*  
操作の[**セキュリティ\_情報**](security-information.md)構造体へのポインター。

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
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの所有者識別子が照会されていることを示します。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのプライマリグループ識別子に対してクエリが行われていることを示します。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの随意アクセス制御リスト (DACL) に対してクエリが行われていることを示します。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのシステム ACL (SACL) に対してクエリが行われていることを示します。 ACCESS_SYSTEM_SECURITY アクセスが必要です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="see-also"></a>関連項目


[**ファイル\_ストリームの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_設定\_セキュリティ**](irp-mj-set-security.md)

[**セキュリティ\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**セキュリティ\_情報**](security-information.md)

 

 







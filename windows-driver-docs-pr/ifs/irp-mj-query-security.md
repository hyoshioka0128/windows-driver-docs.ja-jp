---
title: IRP_MJ_QUERY_SECURITY
description: IRP\_MJ\_クエリ\_セキュリティ
ms.assetid: f0f73bfe-c016-49e2-b725-380f46a9b9d6
keywords:
- IRP_MJ_QUERY_SECURITY インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_SECURITY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01ff2489df4938c97ad3698b7a5dba1f29a82ef9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324532"
---
# <a name="irpmjquerysecurity"></a>IRP\_MJ\_クエリ\_セキュリティ


## <a name="when-sent"></a>送信時


IRP\_MJ\_クエリ\_セキュリティ要求が I/O マネージャーによって送信されます。 送信できる、たとえば、ユーザー モード アプリケーションには、Microsoft Win32 関数が呼び出されるとなど**GetSecurityInfo**します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、ユーザー ファイルを表しますか、ディレクトリを開くかどうかを判断する、ファイル オブジェクトをデコードする必要があります。 場合は、ドライバーは、クエリの処理し、IRP を完了する必要があります。 それ以外の場合、ドライバーでは、クエリを処理することがなく適切な IRP を完了する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のクエリのセキュリティ要求の処理中の IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指定したオブジェクトのセキュリティ記述子のコピーを受け取る呼び出し元が指定の出力バッファーへのポインター。 呼び出し元のプロセスを指定したオブジェクトのセキュリティ状態の側面を表示する権限が必要です。 [**セキュリティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff556610)構造が自己相対形式で返されます。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

Windows xp 以降、ファイル オブジェクトは名前付きのデータ ストリームを表すことができます。 名前付きのデータ ストリームの詳細については、次を参照してください。 [**ファイル\_ストリーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540364)します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_クエリ\_セキュリティ、使用する必要があります。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_クエリ\_セキュリティ。

<a href="" id="irpsp--parameters-querysecurity-length"></a>*IrpSp-&gt;Parameters.QuerySecurity.Length*  
指し示されるバッファーのバイト単位で、サイズ、 *Irp -&gt;UserBuffer*パラメーター。

<a href="" id="irpsp--parameters-querysecurity-securityinformation"></a>*IrpSp-&gt;Parameters.QuerySecurity.SecurityInformation*  
ポインター、 [**セキュリティ\_情報**](security-information.md)操作の構造。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SecurityInformation 値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの所有者の識別子が照会されることを示します。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのプライマリ グループ識別子が照会されることを示します。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの随意アクセス制御リスト (DACL) が照会されることを示します。 READ_CONTROL アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの ACL (SACL)、システムが照会されることを示します。 ACCESS_SYSTEM_SECURITY アクセスが必要です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="see-also"></a>関連項目


[**ファイル\_ストリーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540364)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_SET\_SECURITY**](irp-mj-set-security.md)

[**セキュリティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff556610)

[**セキュリティ\_情報**](security-information.md)

 

 







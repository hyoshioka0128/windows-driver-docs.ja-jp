---
title: IRP_MJ_SET_SECURITY
description: IRP\_MJ\_設定\_セキュリティ
ms.assetid: 8d8b06b9-5d63-4506-831c-9c533dbe95f4
keywords:
- IRP_MJ_SET_SECURITY インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_SET_SECURITY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e810770a0e9ffa085e1d823ddfa9b2f4e2685c24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324236"
---
# <a name="irpmjsetsecurity"></a>IRP\_MJ\_設定\_セキュリティ


## <a name="when-sent"></a>送信時


IRP\_MJ\_設定\_セキュリティ要求が I/O マネージャーによって送信されます。 この要求を送信できますなど、ユーザー モード アプリケーションには、Win32 関数が呼び出されるとなど**SetSecurityInfo**します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、ユーザー ファイルを表しますか、ディレクトリを開くかどうかを判断する、ファイル オブジェクトをデコードする必要があります。 場合は、ドライバーは要求を処理し、IRP を完了する必要があります。 それ以外の場合、ドライバーでは、要求を処理することがなく適切な IRP を完了する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のセットのセキュリティ情報の要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_設定\_セキュリティ、使用する必要があります。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_設定\_セキュリティ。

<a href="" id="irpsp--parameters-setsecurity-securitydescriptor"></a>*IrpSp-&gt;Parameters.SetSecurity.SecurityDescriptor*  
ポインターを[**セキュリティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff556610)オブジェクトに割り当てられるセキュリティ情報の値を含む構造体。

<a href="" id="irpsp--parameters-setsecurity-securityinformation"></a>*IrpSp-&gt;Parameters.SetSecurity.SecurityInformation*  
型の値[**セキュリティ\_情報**](security-information.md)セキュリティを指定する情報は、セキュリティ記述子に設定します。 この値は、次のいずれかを指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SecurityInformation 値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの随意アクセス制御リスト (DACL) が設定されていることを示します。 対する WRITE_DAC アクセス許可が必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのプライマリ グループ id が設定されていることを示します。 WRITE_OWNER アクセスが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトの所有者の識別子が設定されていることを示します。 WRITE_OWNER アクセスが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>オブジェクトのシステム ACL (SACL) が設定されていることを示します。 ACCESS_SYSTEM_SECURITY アクセスが必要です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_QUERY\_SECURITY**](irp-mj-query-security.md)

[**セキュリティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff556610)

[**セキュリティ\_情報**](security-information.md)

 

 







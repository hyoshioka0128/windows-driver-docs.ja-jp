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
ms.openlocfilehash: c669dba96982735b99f9650fb180ea485aca60d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528585"
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

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="deviceobject--flags"></a>*デバイス オブジェクト-&gt;フラグ*  
DO\_バッファーに格納された\_IO、および DO\_直接\_IO フラグを使用するデータは、ドライバーに渡される方法を指定する次のように。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグの設定</th>
<th align="left">I/O メソッド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>~DO_BUFFERED_IO</p>
<p>&amp; ~ DO_DIRECT_IO</p></td>
<td align="left"><p>METHOD_NEITHER</p></td>
</tr>
<tr class="even">
<td align="left"><p>~DO_BUFFERED_IO</p>
<p>&amp; DO_DIRECT_IO</p></td>
<td align="left"><p>METHOD_DIRECT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DO_BUFFERED_IO</p>
<p>&amp; ~ DO_DIRECT_IO</p></td>
<td align="left"><p>METHOD_BUFFERED</p></td>
</tr>
<tr class="even">
<td align="left"><p>DO_BUFFERED_IO</p>
<p>&amp; DO_DIRECT_IO</p></td>
<td align="left"><p>METHOD_BUFFERED</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
システムが指定した場合に、中間システム バッファーとして使用するバッファーへのポインター、DO\_バッファーに格納された\_IO フラグに設定されて*デバイス オブジェクト -&gt;フラグ*。 このメンバーに設定している場合は、 **NULL**します。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
呼び出し元が指定したファイルへのポインター\_クォータ\_をボリュームのクォータ情報を受け取る情報構造の出力バッファー。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_クエリ\_クォータ使用しないでください。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  
このメンバーには、次の 1 つ以上を指定できます。

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
<td align="left"><p>SL_INDEX_SPECIFIED</p></td>
<td align="left"><p>クォータの一覧で指定するインデックスを持つエントリでスキャンを開始<em>IrpSp -&gt;Parameters.QueryQuota.StartSid</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>一覧の最初のエントリでスキャンを開始します。 このフラグが設定されていない場合は、前の IRP_MJ_QUERY_QUOTA 要求からのスキャンを再開します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>見つかった最初のエントリのみを返します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_クエリ\_クォータ。

<a href="" id="irpsp--parameters-queryquota-length"></a>*IrpSp-&gt;Parameters.QueryQuota.Length*  
指すバッファーの長さをバイト単位で*Irp -&gt;UserBuffer*します。

<a href="" id="irpsp--parameters-queryquota-sidlist"></a>*IrpSp-&gt;Parameters.QueryQuota.SidList*  
クォータ情報が返される Sid の一覧への省略可能なポインター。 リスト内の各エントリは、 [**ファイル\_取得\_クォータ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540298)構造体。 この構造体の定義は次のとおりです。

```cpp
typedef struct _FILE_GET_QUOTA_INFORMATION {
    ULONG NextEntryOffset;
    ULONG SidLength;
    SID Sid;
} FILE_GET_QUOTA_INFORMATION, *PFILE_GET_QUOTA_INFORMATION;
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NextEntryOffset</strong></p></td>
<td align="left"><p>複数のエントリが、バッファーに存在する場合は [次へ] の FILE_GET_QUOTA_INFORMATION エントリのバイト オフセット。 この 1 つに後に他のエントリがない場合、このメンバーは 0 を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SidLength</strong></p></td>
<td align="left"><p>(バイト単位) の長さの<strong>Sid</strong>メンバー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sid</strong></p></td>
<td align="left"><p>セキュリティ識別子 (SID)。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-queryquota-sidlistlength"></a>*IrpSp-&gt;Parameters.QueryQuota.SidListLength*  
長さをバイト単位で指定されている場合、Sid の一覧。

<a href="" id="irpsp--parameters-queryquota-startsid"></a>*IrpSp-&gt;Parameters.QueryQuota.StartSid*  
返される情報は、先頭以外のエントリを開始することを示す SID への省略可能なポインター。 SID の一覧が指定されている場合、このパラメーターは無視されます。

## <a name="see-also"></a>関連項目


[**ファイル\_取得\_クォータ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540298)

[**ファイル\_クォータ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540342)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCheckQuotaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548279)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_SET\_QUOTA**](irp-mj-set-quota.md)

 

 







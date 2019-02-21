---
title: IRP_MJ_QUERY_EA
description: IRP\_MJ\_クエリ\_EA
ms.assetid: 5d60a6e9-e940-44cf-844b-86837b36237a
keywords:
- IRP_MJ_QUERY_EA インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_EA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0dd20105e784f942ed8d2b746b521f09b2febc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531930"
---
# <a name="irpmjqueryea"></a>IRP\_MJ\_クエリ\_EA


## <a name="when-sent"></a>送信時


IRP\_MJ\_クエリ\_EA 要求を送信 I/O マネージャーとその他のオペレーティング システムのコンポーネントに加えてその他のカーネル モード ドライバーでは、ユーザー モード アプリケーションは、ファイルに関する情報の拡張を要求されたときに属性。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システムでは、拡張属性をサポートする場合、ファイル システム ドライバーは、クエリの処理し、IRP の完了する必要があります。 状態を返す必要がありますそれ以外の場合、\_EAS\_いない\_サポートされています。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用して\_MJ\_クエリ\_EA 要求。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
中間システム バッファーとして使用するシステム提供の出力バッファーへのポインター。 メソッドの使用\_バッファーに格納された I/O。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
拡張属性の情報を受け取る出力バッファーを記述するメモリ記述子一覧 (MDL) のアドレス。 メソッドの使用\_ダイレクト I/O。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
呼び出し元が指定へのポインター [**ファイル\_完全\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545793)-拡張属性の情報を受け取る構造化した出力バッファー。 メソッドの使用\_どちら I/O。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_クエリ\_EA 使用しないでください。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  
次の値の 1 つ以上を指定します。

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
<td align="left"><p>指定するインデックスを持つ拡張属性の一覧でエントリでスキャンを開始<em>IrpSp -&gt;Parameters.QueryEa.EaIndex</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>一覧の最初のエントリでスキャンを開始します。 このフラグが設定されていない場合は、前の IRP_MJ_QUERY_EA 要求からのスキャンを再開します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>見つかった最初のエントリのみを返します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_クエリ\_EA です。

<a href="" id="irpsp--parameters-queryea-eaindex"></a>*IrpSp-&gt;Parameters.QueryEa.EaIndex*  
拡張属性の一覧をスキャンを開始する位置のエントリのインデックス。 場合、このパラメーターは無視されます、SL\_インデックス\_指定したフラグが設定されていない場合、または*IrpSp -&gt;Parameters.QueryEa.EaList*空でない一覧を示します。

<a href="" id="irpsp--parameters-queryea-ealist"></a>*IrpSp-&gt;Parameters.QueryEa.EaList*  
呼び出し元が指定へのポインター [**ファイル\_取得\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540295)-クエリを実行する拡張属性を指定する構造化の入力バッファー。

<a href="" id="irpsp--parameters-queryea-ealistlength"></a>*IrpSp-&gt;Parameters.QueryEa.EaListLength*  
によって示されるバッファーのバイト長*IrpSp -&gt;Parameters.QueryEa.EaList*します。

<a href="" id="irpsp--parameters-queryea-length"></a>*IrpSp-&gt;Parameters.QueryEa.Length*  
出力バッファーのバイト長。

<a name="remarks"></a>注釈
-------

短いバッファーが指定されると、ステータス\_バッファー\_オーバーフローが返され、NTFS が最後にファイル全体を返します\_完全\_EA\_に合った INFORMATION のエントリ。 短いバッファーが指定されると、状態\_バッファー\_すぎます\_小さなが返され、NTFS には、すべてのファイル収まりきらない\_完全な\_EA\_情報のエントリ。

&gt; \[!注\] &gt; FAT16 が不要になった拡張属性をサポートしている Windows Vista 以降、します。

 

## <a name="see-also"></a>関連項目


[**ファイル\_完全\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545793)

[**ファイル\_取得\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540295)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCheckEaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548252)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_SET\_EA**](irp-mj-set-ea.md)

 

 







---
title: IRP_MJ_QUERY_EA
description: IRP \_ MJ \_ クエリ \_ EA
ms.assetid: 5d60a6e9-e940-44cf-844b-86837b36237a
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_QUERY_EA
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_EA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c5a99e318f0fc23abd6375ceda5e5d427323579
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852067"
---
# <a name="irp_mj_query_ea"></a>IRP \_ MJ \_ クエリ \_ EA


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ QUERY \_ EA 要求は、ユーザーモードアプリケーションがファイルの拡張属性に関する情報を要求したときに、i/o マネージャーと他のオペレーティングシステムコンポーネント、およびその他のカーネルモードドライバーによって送信されます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムで拡張属性がサポートされている場合、ファイルシステムドライバーはクエリを処理し、IRP を完了する必要があります。 それ以外の場合は、ステータス EAS がサポートされ \_ \_ ていない状態を返し \_ ます。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、irp \_ MJ QUERY EA 要求の処理中に、irp の次のメンバーと irp スタックの場所に設定されている情報を使用でき \_ \_ ます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt; AssociatedIrp*  
中間システムバッファーとして使用されるシステム指定の出力バッファーへのポインター。 メソッドバッファー i/o に使用され \_ ます。

<a href="" id="irp--iostatus"></a>*Irp- &gt; iostatus*  
最終的な完了ステータスと要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; mdladdress*  
拡張属性情報を受け取る出力バッファーを記述するメモリ記述子リスト (MDL) のアドレス。 メソッドダイレクト i/o に使用され \_ ます。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
拡張属性情報を受け取る、呼び出し元によって提供されるファイルへのポインター。 [** \_ 完全 \_ EA \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)が構造化された出力バッファーです。 I/o ではないメソッドに対して使用され \_ ます。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイルオブジェクト構造の "関連性のある**fileobject** " フィールド \_ は、IRP MJ QUERY EA の処理中は無効であり、 \_ \_ \_ 使用しないでください。

<a href="" id="irpsp--flags"></a>*IrpSp- &gt; フラグ*  
次の値のうち1つ以上を指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_INDEX_SPECIFIED</p></td>
<td align="left"><p>インデックスが指定されている拡張属性の一覧のエントリから、" <em>Irpsp- &gt; パラメーター</em>" でスキャンを開始します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>一覧の最初のエントリからスキャンを開始します。 このフラグが設定されていない場合は、以前の IRP_MJ_QUERY_EA 要求からスキャンを再開します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>最初に見つかったエントリだけを返します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
IRP \_ MJ QUERY EA を指定し \_ \_ ます。

<a href="" id="irpsp--parameters-queryea-eaindex"></a>*IrpSp- &gt; パラメーター. Quer. e:*  
拡張属性リストのスキャンを開始する位置のエントリのインデックス。 このパラメーターは、 \_ \_ 指定された SL インデックスフラグが設定されていない場合や、 *irpsp &gt; パラメーター*が空でないリストを指している場合は無視されます。

<a href="" id="irpsp--parameters-queryea-ealist"></a>*IrpSp- &gt; パラメーター。 EaList*  
呼び出し元から提供されるファイルへのポインターは、クエリ対象の拡張属性を指定する[** \_ \_ EA \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_ea_information)で構成された入力バッファーを取得します。

<a href="" id="irpsp--parameters-queryea-ealistlength"></a>*IrpSp- &gt; パラメーター。この値は、*  
Irpsp によってポイントされたバッファーの長さ (バイト単位)。 * &gt; Quer. ealist*。

<a href="" id="irpsp--parameters-queryea-length"></a>*Irpsp- &gt; パラメーター. quer*  
出力バッファーの長さ (バイト単位)。

<a name="remarks"></a>コメント
-------

短いバッファーが指定され、ステータス \_ バッファーの \_ オーバーフローが返されると、NTFS は最後にファイル全体の \_ 完全な \_ EA 情報のエントリを返し \_ ます。 短いバッファーが指定されていて、ステータス \_ バッファー \_ が小さすぎる場合 \_ 、NTFS は \_ 完全な \_ EA \_ 情報エントリをすべてファイルに収めることができませんでした。

> [!NOTE]
> Windows Vista 以降では、FAT16 は拡張属性をサポートしなくなりました。

 

## <a name="see-also"></a>関連項目


[**\_EA の完全な \_ \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**ファイル \_ の \_ EA \_ 情報の取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_ea_information)

[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ SET \_ EA**](irp-mj-set-ea.md)

 

 







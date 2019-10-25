---
title: IRP_MJ_QUERY_EA
description: IRP\_MJ\_クエリ\_EA
ms.assetid: 5d60a6e9-e940-44cf-844b-86837b36237a
keywords:
- IRP_MJ_QUERY_EA インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_EA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e40b69d0602c055d4522e31241dfdd92c643b52
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841168"
---
# <a name="irp_mj_query_ea"></a>IRP\_MJ\_クエリ\_EA


## <a name="when-sent"></a>送信時


IRP\_MJ\_QUERY\_EA 要求は、ユーザーモードアプリケーションがファイルの拡張属性に関する情報を要求したときに、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムで拡張属性がサポートされている場合、ファイルシステムドライバーはクエリを処理し、IRP を完了する必要があります。 それ以外の場合は、状態\_EAS\_返され\_サポートされていません。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、irp の次のメンバーで設定されている情報を使用することができます、irp\_MJ\_クエリ\_EA 要求を処理します。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
中間システムバッファーとして使用されるシステム指定の出力バッファーへのポインター。 メソッド\_バッファー i/o に使用されます。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最後の完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
拡張属性情報を受け取る出力バッファーを記述するメモリ記述子リスト (MDL) のアドレス。 メソッド\_直接 i/o に使用されます。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
拡張属性情報を受け取る[ **\_EA\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)構造化出力バッファー\_、呼び出し元が提供するファイルへのポインター。 I/o ではない\_メソッドに使用されます。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ\_QUERY\_EA の処理中は、ファイル\_オブジェクト構造の関連性の**あるフィールドは**無効であり、使用できません。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  
次の値のうち1つ以上を指定します。

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
<td align="left"><p><em>Irpsp-&gt;パラメーター</em>によってインデックスが指定されている拡張属性リストのエントリで、スキャンを開始します。</p></td>
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

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
EA\_\_\_のクエリを実行するように指定します。

<a href="" id="irpsp--parameters-queryea-eaindex"></a>*IrpSp-&gt;パラメーターです。*  
拡張属性リストのスキャンを開始する位置のエントリのインデックス。 SL\_インデックス\_指定されたフラグが設定されていない場合、または*Irpsp-&gt;パラメーター*が空でないリストを指している場合、このパラメーターは無視されます。

<a href="" id="irpsp--parameters-queryea-ealist"></a>*IrpSp-&gt;パラメーターです。*  
クエリ対象の拡張属性を指定する[ **\_EA\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_ea_information)を構造化した入力バッファー\_取得する、呼び出し元によって提供されるファイルへのポインター。

<a href="" id="irpsp--parameters-queryea-ealistlength"></a>*IrpSp-&gt;パラメーター。この値は、*  
Irpsp-&gt;パラメーターが指すバッファーの長さ (バイト単位) *。 Quer. EaList*.

<a href="" id="irpsp--parameters-queryea-length"></a>*IrpSp-&gt;パラメーター。この値は、*  
出力バッファーの長さ (バイト単位)。

<a name="remarks"></a>注釈
-------

短いバッファーが指定され、状態\_バッファー\_オーバーフローが返された場合、NTFS は最後のファイル\_完全なファイル全体を返します。完全\_EA\_情報に一致します。 短いバッファーが指定されていて、状態\_バッファーの\_が小さすぎ\_返された場合、NTFS はすべてのファイル\_完全\_EA\_情報エントリを収めることができませんでした。

&gt; \[!注\] &gt; Windows Vista 以降では、FAT16 は拡張属性をサポートしなくなりました。

 

## <a name="see-also"></a>関連項目


[**ファイル\_EA\_の完全\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**ファイル\_\_EA\_情報を取得する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_ea_information)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_設定\_EA**](irp-mj-set-ea.md)

 

 







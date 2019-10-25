---
title: IRP_MJ_SET_EA
description: IRP\_MJ\_設定\_EA
ms.assetid: f9e1f867-a473-46ac-a1c0-63534c4c0755
keywords:
- IRP_MJ_SET_EA インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_SET_EA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 156e45f78295dd5b1c42cbee234c92bdb7f3f6fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841152"
---
# <a name="irp_mj_set_ea"></a>IRP\_MJ\_設定\_EA


## <a name="when-sent"></a>送信時


I/o マネージャーは、ファイルの拡張属性を設定するために、IRP\_MJ\_SET\_EA 要求を送信します。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムが拡張属性をサポートしている場合は、ファイルシステムドライバーが要求を処理し、IRP を完了する必要があります。 それ以外の場合、ファイルシステムドライバーは **\_サポートされていない\_EAS\_ステータス**を返す必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、set extended attributes 要求の処理で、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
設定する拡張属性情報が格納されているシステム指定の入力バッファーへのポインター。 メソッド\_バッファー i/o に使用されます。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
拡張属性情報を受け取る入力バッファーを記述するメモリ記述子リスト (MDL) のアドレス。 メソッド\_直接 i/o に使用されます。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
呼び出し元が指定したファイルへのポインター [ **\_完全\_EA\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)拡張属性情報を受け取る情報構造化入力バッファーです。 I/o ではない\_メソッドに使用されます。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_obect 構造体でもあります。 ファイル\_オブジェクト構造の\_の対象となるフィールドは、IRP\_MJ の処理中は無効**であり、** EA\_設定されているため、使用できません。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
EA\_設定\_IRP\_MJ を指定します。

<a href="" id="irpsp--parameters-setea-length"></a>*IrpSp-&gt;Parameters. SetEa. 長さ*  
入力バッファーの長さ (バイト単位)。

## <a name="see-also"></a>関連項目


[**ファイル\_EA\_の完全\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クエリ\_EA**](irp-mj-query-ea.md)

 

 







---
title: IRP_MJ_SET_EA
description: IRP\_MJ\_設定\_EA
ms.assetid: f9e1f867-a473-46ac-a1c0-63534c4c0755
keywords:
- IRP_MJ_SET_EA インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_SET_EA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd2716e9a9b385f4f9772c3c4972e394669c6eb6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324372"
---
# <a name="irpmjsetea"></a>IRP\_MJ\_設定\_EA


## <a name="when-sent"></a>送信時


I/O マネージャー送信 IRP\_MJ\_設定\_EA 要求ファイルを設定するには属性の拡張します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システムでは、拡張属性をサポートする場合、ファイル システム ドライバーは要求を処理し、IRP を完了する必要があります。 ファイル システム ドライバーを返す必要がありますそれ以外の場合、**状態\_EAS\_いない\_サポートされている**します。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のセットの拡張属性の要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
拡張属性情報設定を含むシステム提供の入力バッファーへのポインター。 メソッドの使用\_バッファーに格納された I/O。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
拡張属性の情報を受け取る入力のバッファーを記述するメモリ記述子一覧 (MDL) のアドレス。 メソッドの使用\_ダイレクト I/O。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
呼び出し元が指定へのポインター [**ファイル\_完全\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545793)-拡張属性の情報を受け取る入力バッファーを構造化します。 メソッドの使用\_どちら I/O。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_設定\_EA 使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_設定\_EA です。

<a href="" id="irpsp--parameters-setea-length"></a>*IrpSp-&gt;Parameters.SetEa.Length*  
入力バッファーのバイト長。

## <a name="see-also"></a>関連項目


[**ファイル\_完全\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545793)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCheckEaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548252)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_クエリ\_EA**](irp-mj-query-ea.md)

 

 







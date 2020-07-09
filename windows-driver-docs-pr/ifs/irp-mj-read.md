---
title: IRP_MJ_READ (IFS)
description: IRP_MJ_READ
ms.assetid: f2f909ff-4af6-433e-9f3c-9692b5ab7171
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_READ
topic_type:
- apiref
api_name:
- IRP_MJ_READ
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b97209bd720be7157fa1ff3778240389d3d773bc
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141230"
---
# <a name="irp_mj_read-ifs"></a>IRP \_ MJ \_ READ (IFS)


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ READ 要求は、i/o マネージャーまたはファイルシステムドライバーによって送信されます。 この要求は、たとえば、ユーザーモードアプリケーションが**ReadFile**などの Microsoft Win32 関数を呼び出したとき、またはカーネルモードコンポーネントが[**zwreadfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)を呼び出したときに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、パラメーターとマイナー関数コードを決定するために、ファイルオブジェクトを抽出してデコードする必要があります。

メモリ記述子リスト (MDL) の読み取り要求では、ファイルシステムがマイナー関数コードを確認して、どの操作が要求されているかを判断する必要があります。 有効なマイナー関数コードを次に示します。これらは、キャッシュされたファイル i/o に対してのみ使用できます。

- IRP \_ \_ 完了完了

- IRP \_ \_ 完全完了 \_ MDL

- IRP \_ の \_ 包括的な \_ MDL \_ DPC

- IRP \_ \_ 圧縮済み

- IRP の全 \_ \_ DPC

- IRP の全 \_ \_ MDL

- IRP の全 \_ \_ MDL \_ DPC

- IRP \_ \_ 通常

この IRP の処理の詳細については、Windows Driver Kit (WDK) に含まれている CDFS と FASTFAT のサンプルを参照してください。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは必要な処理を実行し、フィルターの性質に応じて、IRP を完了するか失敗させるか、スタック上の次の下位のドライバーに渡します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、次の IRP のメンバーと IRP スタックの場所に含まれている情報を読み取り要求の処理中に使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  

ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp &gt;AssociatedIrp.SystemBuffer*  

実行バッファー \_ \_ IO フラグが*DeviceObject に &gt; *設定されている場合、中間システムバッファーとして使用されるシステム指定のバッファーへのポインター。 それ以外の場合、このメンバーは**NULL**に設定されます。

<a href="" id="irp--iostatus"></a>*Irp- &gt; iostatus*  

最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。 詳細については、「 [**Zwreadfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)への*iostatusblock*パラメーターの説明」を参照してください。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; mdladdress*  

読み取るデータを含むページを記述するメモリ記述子リスト (MDL) のアドレス。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  

ファイルから読み取られたデータを受け取る、呼び出し元から提供される出力バッファーへのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  

*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。 FO \_ 同期 \_ IO フラグが*irpsp- &gt; &gt; Flags*で設定されている場合、ファイルオブジェクトは同期 i/o 用に開かれています。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 **RelatedFileObject** \_ IRP MJ READ の処理中は、ファイルオブジェクト構造の "関連性のある fileobject" フィールドは無効です \_ 。使用しないで \_ ください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  

IRP MJ READ を指定し \_ \_ ます。

<a href="" id="irpsp--minorfunction"></a>*IrpSp- &gt; minorfunction*  

要求される操作を指定し、次のいずれかを含みます。

- IRP \_ \_ 完了完了

- IRP \_ \_ 完全完了 \_ MDL

- IRP \_ の \_ 包括的な \_ MDL \_ DPC

- IRP \_ \_ 圧縮済み

- IRP の全 \_ \_ DPC

- IRP の全 \_ \_ MDL

- IRP の全 \_ \_ MDL \_ DPC

- IRP \_ \_ 通常

<a href="" id="irpsp--parameters-read-byteoffset"></a>*IrpSp- &gt; Parameters。読み取りバイトオフセット*

\_読み取るデータのファイル内での開始バイトオフセットを指定する大きな整数変数。

<a href="" id="irpsp--parameters-read-key"></a>*IrpSp- &gt; Parameters. Read. Key*

ターゲットファイルのバイト範囲ロックに関連付けられたキー値。

<a href="" id="irpsp--parameters-read-length"></a>*IrpSp- &gt; Parameters、Read. Length*

読み取るデータの長さ (バイト単位)。 読み取り操作が成功した場合は、 *Irp- &gt; iostatus*が指す[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体の**情報**メンバーに読み取られたバイト数が返されます。

<a name="remarks"></a>解説
-------

ファイルシステムは、ファイルの最後に、基になるファイルストレージデバイスのセクターサイズの倍数まで、書き込み操作と読み取り操作を実行します。 読み取り前または書き込み前の操作を処理する場合、バッファーの割り当てとスワップを行うフィルターでは、割り当てられたバッファーのサイズを、関連付けられているデバイスのセクターサイズの倍数まで丸める必要があります。 そうでない場合は、基になるファイルシステムから転送されるデータの長さが、バッファーに割り当てられた長さを超えます。 バッファーのスワップの詳細については、「 [Swapbuffers のミニサンプル](https://go.microsoft.com/fwlink/p/?linkid=256055)」を参照してください。

## <a name="see-also"></a>関連項目


[**CcMdlRead**](https://docs.microsoft.com/previous-versions/ff539159(v=vs.85))

[**CcMdlReadComplete**](https://msdn.microsoft.com/library/windows/hardware/ff539163)

[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ READ (WDK カーネルリファレンス)**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)

[**IRP \_ MJ \_ 書き込み**](irp-mj-write.md)

[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)

 

 







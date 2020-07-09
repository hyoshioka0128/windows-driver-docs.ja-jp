---
title: IRP_MJ_WRITE (IFS)
description: IRP_MJ_WRITE
ms.assetid: 8f16a579-1598-4f70-8d88-dfe877daec31
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_WRITE
topic_type:
- apiref
api_name:
- IRP_MJ_WRITE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f6de72c2b7be99c0abc426d1e0811bf3ec3f88a
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141224"
---
# <a name="irp_mj_write-ifs"></a>IRP \_ MJ \_ WRITE (IFS)


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ 書き込み要求は、i/o マネージャーまたはファイルシステムドライバーによって送信されます。 この要求は、たとえば、ユーザーモードアプリケーションが**WriteFile**などの Microsoft Win32 関数を呼び出したときや、カーネルモードコンポーネントが[**zwwritefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)を呼び出したときに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、パラメーターとマイナー関数コードを決定するために、ファイルオブジェクトを抽出してデコードする必要があります。

MDL 書き込み要求の場合、ファイルシステムはマイナー関数コードを確認して、どの操作が要求されているかを判断する必要があります。 有効なマイナー関数コードを次に示します。これらは、キャッシュされたファイル i/o に対してのみ使用できます。

- IRP \_ \_ 完了完了

- IRP \_ \_ 完全完了 \_ MDL

- IRP \_ の \_ 包括的な \_ MDL \_ DPC

- IRP \_ \_ 圧縮済み

- IRP の全 \_ \_ DPC

- IRP の全 \_ \_ MDL

- IRP の全 \_ \_ MDL \_ DPC

- IRP \_ \_ 通常

この IRP を処理する方法の詳細については、Windows Driver Kit (WDK) に含まれている FASTFAT サンプルを調べてください。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、必要な処理を実行する必要があります。フィルターの性質に応じて、IRP を完了するか失敗させるか、またはスタック上の次の下位のドライバーに渡します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、create 要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  

ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp &gt;AssociatedIrp.SystemBuffer*  

\_ \_ * &gt; DeviceObject*にバッファリング IO フラグが設定されている場合、中間システムバッファーとして使用されるシステム指定のバッファーへのポインター。 それ以外の場合、このメンバーは**NULL**に設定されます。

<a href="" id="irp--iostatus"></a>*Irp- &gt; iostatus*  

最終的な完了ステータスと要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。 IRP \_ MJ 書き込み要求が失敗した場合 \_ 、ファイルシステムの書き込みディスパッチルーチンはエラー NTSTATUS 値を返し、 *irp- &gt; iostatus*の値を返します。情報は定義されていないため、使用しないでください。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; mdladdress*  

データの書き込み先のページを記述するメモリ記述子リスト (MDL) のアドレス。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*

*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。 FO \_ 同期 \_ IO フラグが*irpsp- &gt; &gt; Flags*で設定されている場合、ファイルオブジェクトは同期 i/o 用に開かれています。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイルオブジェクト構造の MJ **fileobject**フィールド \_ は、IRP WRITE の処理中は無効であり、 \_ 使用でき \_ ません。

<a href="" id="irpsp--flags"></a>*IrpSp- &gt; フラグ*  

SL \_ FORCE \_ ダイレクト \_ 書き込みフラグが設定されている場合、カーネルモードドライバーは、直接書き込みをブロックしているために通常は書き込むことができないボリューム領域に書き込むことができます。 Windows Vista 以降のオペレーティングシステムでは、セキュリティ上の理由により、直接書き込みのブロックが実装されました。 このフラグは、ファイルシステムレイヤーとストレージスタックレイヤーの両方でチェックされます。 直接書き込みブロックの詳細については、「[ボリュームとディスクへの直接書き込み操作のブロック](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。 SL \_ FORCE \_ ダイレクト \_ 書き込みフラグは、windows Vista 以降のバージョンの windows で使用できます。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*

IRP MJ WRITE を指定し \_ \_ ます。

<a href="" id="irpsp--minorfunction"></a>*IrpSp- &gt; minorfunction*  

要求される操作を指定し、次のいずれかを含みます。

-   IRP \_ \_ 完了完了

-   IRP \_ \_ 完全完了 \_ MDL

-   IRP \_ の \_ 包括的な \_ MDL \_ DPC

-   IRP \_ \_ 圧縮済み

-   IRP の全 \_ \_ DPC

-   IRP の全 \_ \_ MDL

-   IRP の全 \_ \_ MDL \_ DPC

-   IRP \_ \_ 通常

<a href="" id="irpsp--parameters-write-byteoffset"></a>*IrpSp- &gt; Parameters。書き込み。 ByteOffset*  

\_書き込むデータのファイル内での開始バイトオフセットを指定する大きな整数変数。

特定の状況では、このパラメーターに特別な値が含まれる場合があります。 次に例を示します。

-   次の条件に該当する場合は、ファイルの現在の終わりを明示的なファイルオフセット値の代わりに使用する必要があることを示します。

    *Irpsp- &gt;Parameters.. ByteOffset. LowPart* = = \_ \_ \_ \_ ファイルの終わりへのファイルの書き込み \_ と*irpsp の書き込み。 &gt; highpart* = =-1

<a href="" id="irpsp--parameters-write-key"></a>*IrpSp- &gt; Parameters. Write. Key*  

ターゲットファイルのバイト範囲ロックに関連付けられたキー値。

<a href="" id="irpsp--parameters-write-length"></a>*IrpSp- &gt; Parameters. Write. Length*  

書き込まれるデータの長さ (バイト単位)。 書き込み操作が成功すると、書き込まれたバイト数が、 **Information** \_ \_ *Irp- &gt; iostatus*によって示された IO 状態ブロック構造体の情報メンバーに返されます。

<a name="remarks"></a>解説
-------

ファイルシステムは、ファイルの最後に、基になるファイルストレージデバイスのセクターサイズの倍数まで、書き込み操作と読み取り操作を実行します。 読み取り前または書き込み前の操作を処理する場合、バッファーの割り当てとスワップを行うフィルターでは、割り当てられたバッファーのサイズを、関連付けられているデバイスのセクターサイズの倍数まで丸める必要があります。 そうでない場合は、基になるファイルシステムから転送されるデータの長さが、バッファーに割り当てられた長さを超えます。 バッファーのスワップの詳細については、「 [Swapbuffers のミニサンプル](https://go.microsoft.com/fwlink/p/?linkid=256055)」を参照してください。

## <a name="see-also"></a>関連項目


[**CcMdlWriteComplete**](https://msdn.microsoft.com/library/windows/hardware/ff539172)

[**Cc/Mdlwrite**](https://msdn.microsoft.com/library/windows/hardware/ff539181)

[**FLT \_ IO \_ パラメーター \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ の \_ 読み取り**](irp-mj-read.md)

[**IRP \_ MJ \_ WRITE (WDK カーネルリファレンス)**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)

[**ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)

 

 







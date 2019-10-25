---
title: IRP_MJ_WRITE
description: IRP_MJ_WRITE
ms.assetid: 8f16a579-1598-4f70-8d88-dfe877daec31
keywords:
- IRP_MJ_WRITE インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_WRITE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd68e4a7e392d0758702f759e3b8981278ce8c42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841144"
---
# <a name="irp_mj_write"></a>IRP\_MJ\_WRITE


## <a name="when-sent"></a>送信時


IRP\_MJ\_書き込み要求は、i/o マネージャーまたはファイルシステムドライバーによって送信されます。 この要求は、たとえば、ユーザーモードアプリケーションが**WriteFile**などの Microsoft Win32 関数を呼び出したときや、カーネルモードコンポーネントが[**zwwritefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)を呼び出したときに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、パラメーターとマイナー関数コードを決定するために、ファイルオブジェクトを抽出してデコードする必要があります。

MDL 書き込み要求の場合、ファイルシステムはマイナー関数コードを確認して、どの操作が要求されているかを判断する必要があります。 有効なマイナー関数コードを次に示します。これらは、キャッシュされたファイル i/o に対してのみ使用できます。

- IRP\_完了\_完了

- IRP\_\_完了\_MDL

- IRP\_\_完了\_MDL\_DPC

- IRP\_\_圧縮

- IRP\_\_DPC

- IRP\_\_MDL

- IRP\_\_MDL\_DPC

- IRP\_通常\_

この IRP を処理する方法の詳細については、Windows Driver Kit (WDK) に含まれている FASTFAT サンプルを調べてください。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、必要な処理を実行する必要があります。フィルターの性質に応じて、IRP を完了するか失敗させるか、またはスタック上の次の下位のドライバーに渡します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、create 要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  

ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  

\_バッファー\_IO フラグが*DeviceObject-&gt;フラグ*で設定されている場合に、中間システムバッファーとして使用されるシステム指定のバッファーへのポインター。 それ以外の場合、このメンバーは**NULL**に設定されます。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  

最後の完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。 IRP\_MJ\_書き込み要求が失敗した場合、ファイルシステムの書き込みディスパッチルーチンはエラー NTSTATUS 値を返し、 *irp&gt;IoStatus*の値を返します。情報は定義されていないため、使用しないでください。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  

データの書き込み先のページを記述するメモリ記述子リスト (MDL) のアドレス。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*

*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。 FO\_同期\_IO フラグが*Irpsp-&gt;の&gt;FileObject フラグ*で設定されている場合、ファイルオブジェクトは同期 i/o 用に開かれています。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ\_WRITE の処理中は、ファイル\_オブジェクト構造の関連性の**あるフィールドは**無効であり、使用できません。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  

SL\_強制\_ダイレクト\_書き込みフラグが設定されている場合、カーネルモードドライバーは、直接書き込みをブロックしているために通常は書き込むことができないボリューム領域に書き込むことができます。 Windows Vista 以降のオペレーティングシステムでは、セキュリティ上の理由により、直接書き込みのブロックが実装されました。 このフラグは、ファイルシステムレイヤーとストレージスタックレイヤーの両方でチェックされます。 直接書き込みブロックの詳細については、「[ボリュームとディスクへの直接書き込み操作のブロック](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。 SL\_FORCE\_ダイレクト\_書き込みフラグは、windows Vista 以降のバージョンの Windows で使用できます。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*

IRP\_MJ\_書き込むことを指定します。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  

要求される操作を指定し、次のいずれかを含みます。

-   IRP\_完了\_完了

-   IRP\_\_完了\_MDL

-   IRP\_\_完了\_MDL\_DPC

-   IRP\_\_圧縮

-   IRP\_\_DPC

-   IRP\_\_MDL

-   IRP\_\_MDL\_DPC

-   IRP\_通常\_

<a href="" id="irpsp--parameters-write-byteoffset"></a>*IrpSp-&gt;のパラメーターです。 ByteOffset を書き込みます。*  

書き込むデータのファイル内の開始バイトオフセットを指定する、大きな\_整数変数。

特定の状況では、このパラメーターに特別な値が含まれる場合があります。 次に、例を示します。

-   次の条件に該当する場合は、ファイルの現在の終わりを明示的なファイルオフセット値の代わりに使用する必要があることを示します。

    *Irpsp-&gt;parameters. ByteOffset. LowPart* = = ファイル\_\_ファイルと*Irpsp-\_パラメーター*の\_エンド&gt;に\_書き込みます。 Byteoffset. highpart = =-1

<a href="" id="irpsp--parameters-write-key"></a>*IrpSp-&gt;のパラメーターです。キー*  

ターゲットファイルのバイト範囲ロックに関連付けられたキー値。

<a href="" id="irpsp--parameters-write-length"></a>*IrpSp-&gt;Parameters. Write. Length*  

書き込まれるデータの長さ (バイト単位)。 書き込み操作が成功すると、書き込まれたバイト数が、 *Irp&gt;IoStatus*によって示される IO\_ステータス\_ブロック構造の**情報**メンバーに返されます。

<a name="remarks"></a>注釈
-------

ファイルシステムは、ファイルの最後に、基になるファイルストレージデバイスのセクターサイズの倍数まで、書き込み操作と読み取り操作を実行します。 読み取り前または書き込み前の操作を処理する場合、バッファーの割り当てとスワップを行うフィルターでは、割り当てられたバッファーのサイズを、関連付けられているデバイスのセクターサイズの倍数まで丸める必要があります。 そうでない場合は、基になるファイルシステムから転送されるデータの長さが、バッファーに割り当てられた長さを超えます。 バッファーのスワップの詳細については、「 [Swapbuffers のミニサンプル](https://go.microsoft.com/fwlink/p/?linkid=256055)」を参照してください。

## <a name="see-also"></a>関連項目


[**CcMdlWriteComplete**](https://msdn.microsoft.com/library/windows/hardware/ff539172)

[**Cc/Mdlwrite**](https://msdn.microsoft.com/library/windows/hardware/ff539181)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_読み取り**](irp-mj-read.md)

[**IRP\_MJ\_WRITE (WDK カーネルリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)

[**ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)

 

 







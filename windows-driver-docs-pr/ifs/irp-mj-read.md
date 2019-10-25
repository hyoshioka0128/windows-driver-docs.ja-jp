---
title: IRP_MJ_READ
description: IRP_MJ_READ
ms.assetid: f2f909ff-4af6-433e-9f3c-9692b5ab7171
keywords:
- IRP_MJ_READ インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_READ
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 345a6d927621531b81a0d272722cb35ea9bd2ac6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841155"
---
# <a name="irp_mj_read"></a>IRP\_MJ\_READ


## <a name="when-sent"></a>送信時


IRP\_MJ\_読み取り要求は、i/o マネージャーまたはファイルシステムドライバーによって送信されます。 この要求は、たとえば、ユーザーモードアプリケーションが**ReadFile**などの Microsoft Win32 関数を呼び出したとき、またはカーネルモードコンポーネントが[**zwreadfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)を呼び出したときに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、パラメーターとマイナー関数コードを決定するために、ファイルオブジェクトを抽出してデコードする必要があります。

メモリ記述子リスト (MDL) の読み取り要求では、ファイルシステムがマイナー関数コードを確認して、どの操作が要求されているかを判断する必要があります。 有効なマイナー関数コードを次に示します。これらは、キャッシュされたファイル i/o に対してのみ使用できます。

- IRP\_完了\_完了

- IRP\_\_完了\_MDL

- IRP\_\_完了\_MDL\_DPC

- IRP\_\_圧縮

- IRP\_\_DPC

- IRP\_\_MDL

- IRP\_\_MDL\_DPC

- IRP\_通常\_

この IRP の処理の詳細については、Windows Driver Kit (WDK) に含まれている CDFS と FASTFAT のサンプルを参照してください。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは必要な処理を実行し、フィルターの性質に応じて、IRP を完了するか失敗させるか、スタック上の次の下位のドライバーに渡します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、次の IRP のメンバーと IRP スタックの場所に含まれている情報を読み取り要求の処理中に使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  

ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  

\_バッファー\_IO フラグが*DeviceObject-&gt;フラグ*で設定されている場合に、中間システムバッファーとして使用されるシステム指定のバッファーへのポインター。 それ以外の場合、このメンバーは**NULL**に設定されます。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  

最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。 詳細については、「 [**Zwreadfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)への*iostatusblock*パラメーターの説明」を参照してください。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  

読み取るデータを含むページを記述するメモリ記述子リスト (MDL) のアドレス。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  

ファイルから読み取られたデータを受け取る、呼び出し元から提供される出力バッファーへのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  

*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。 FO\_同期\_IO フラグが*Irpsp-&gt;の&gt;FileObject フラグ*で設定されている場合、ファイルオブジェクトは同期 i/o 用に開かれています。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_obect 構造体でもあります。 IRP\_MJ\_の処理中は、ファイル\_オブジェクト構造の関連性のあるフィールドは無効で**あり、使用**できません。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  

IRP\_MJ\_読み取ることを指定します。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  

要求される操作を指定し、次のいずれかを含みます。

- IRP\_完了\_完了

- IRP\_\_完了\_MDL

- IRP\_\_完了\_MDL\_DPC

- IRP\_\_圧縮

- IRP\_\_DPC

- IRP\_\_MDL

- IRP\_\_MDL\_DPC

- IRP\_通常\_

<a href="" id="irpsp--parameters-read-byteoffset"></a>*IrpSp-&gt;のパラメーターです。 ByteOffset を読み取ります。*

読み取るデータのファイル内の開始バイトオフセットを指定する、大きな\_整数変数。

<a href="" id="irpsp--parameters-read-key"></a>*IrpSp-&gt;パラメーター。読み取り。キー*

ターゲットファイルのバイト範囲ロックに関連付けられたキー値。

<a href="" id="irpsp--parameters-read-length"></a>*IrpSp-&gt;のパラメーターです。長さを読み取ります。*

読み取るデータの長さ (バイト単位)。 読み取り操作が成功した場合は、 [**i/o\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造の**情報**メンバーに読み取られたバイト数が返されます。これは、 *Irp&gt;iostatus*によって示されます。

<a name="remarks"></a>注釈
-------

ファイルシステムは、ファイルの最後に、基になるファイルストレージデバイスのセクターサイズの倍数まで、書き込み操作と読み取り操作を実行します。 読み取り前または書き込み前の操作を処理する場合、バッファーの割り当てとスワップを行うフィルターでは、割り当てられたバッファーのサイズを、関連付けられているデバイスのセクターサイズの倍数まで丸める必要があります。 そうでない場合は、基になるファイルシステムから転送されるデータの長さが、バッファーに割り当てられた長さを超えます。 バッファーのスワップの詳細については、「 [Swapbuffers のミニサンプル](https://go.microsoft.com/fwlink/p/?linkid=256055)」を参照してください。

## <a name="see-also"></a>関連項目


[**CcMdlRead**](https://docs.microsoft.com/previous-versions/ff539159(v=vs.85))

[**CcMdlReadComplete**](https://msdn.microsoft.com/library/windows/hardware/ff539163)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_読み取り (WDK カーネルリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)

[**IRP\_MJ\_書き込み**](irp-mj-write.md)

[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)

 

 







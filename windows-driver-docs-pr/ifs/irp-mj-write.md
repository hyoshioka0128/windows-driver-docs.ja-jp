---
title: IRP_MJ_WRITE
description: IRP_MJ_WRITE
ms.assetid: 8f16a579-1598-4f70-8d88-dfe877daec31
keywords:
- IRP_MJ_WRITE インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_WRITE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7a9867fb75d40cc8cba61375f0c07544fa0613d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375668"
---
# <a name="irpmjwrite"></a>IRP\_MJ\_WRITE


## <a name="when-sent"></a>送信時


IRP\_MJ\_書き込み I/O マネージャーによって、またはファイル システム ドライバーによって要求が送信されます。 この要求を送信できますなど、ユーザー モード アプリケーションには、Microsoft Win32 関数が呼び出されるとなど**WriteFile**カーネル モード コンポーネントが呼び出されたときまたは[ **ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile).

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、パラメーターおよびマイナーの関数コードを確認するファイル オブジェクトをデコードする必要があります。

MDL 書き込み要求、ファイル システムは必要な操作を決定するマイナー関数コードを確認する必要があります。 次に、キャッシュされたファイルの I/O に対してのみ使用できる有効なマイナー関数コードを示します。

- IRP\_MN\_完了

- IRP\_MN\_完了\_MDL

- IRP\_MN\_完了\_MDL\_DPC

- IRP\_MN\_圧縮

- IRP\_MN\_DPC

- IRP\_MN\_MDL

- IRP\_MN\_MDL\_DPC

- IRP\_MN\_標準

この IRP の処理方法の詳細については、Windows Driver Kit (WDK) で含まれている FASTFAT サンプルを調べます。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、必要な処理を実行、フィルターの性質によってすべて完了して、IRP の失敗またはかスタック上の次の下位ドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP スタックの場所を作成する要求の処理では、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  

ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  

場合に、中間システム バッファーとして使用するシステム提供されているバッファーへのポインター、DO\_バッファーに格納された\_IO フラグに設定されて*デバイス オブジェクト -&gt;フラグ*します。 このメンバーに設定している場合は、 **NULL**します。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  

ポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)最終的な完了の状態と、要求された操作に関する情報を受け取る。 場合、IRP\_MJ\_書き込み要求が失敗した場合、ファイル システムの書き込みのディスパッチ ルーチンがエラー NTSTATUS 値、およびの値を返します*Irp -&gt;IoStatus.Information*は未定義とすることはできませんこのオプションを使用するとします。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  

データが書き込まれるページを記述したメモリ記述子一覧 (MDL) のアドレス。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*

関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。 場合、FO\_同期\_IO フラグに設定されて*IrpSp -&gt;FileObject -&gt;フラグ*、同期 I/O 用に、ファイル オブジェクトが開かれました。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_書き込みし、は使用できません。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  

場合、SL\_FORCE\_直接\_書き込みフラグが設定されて、カーネル モード ドライバーがボリュームの領域に書き込むことができますを通常書き込むことができないため直接ブロックを記述します。 Windows Vista 以降のオペレーティング システムでセキュリティ上の理由から、直接書き込みブロックが実装されました。 ファイル システム レイヤーと記憶域スタック レイヤーの両方でこのフラグをチェックします。 直接書き込みのブロックに関する詳細については、次を参照してください。[ボリュームとディスクに直接書き込みの操作をブロックしている](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 SL\_FORCE\_直接\_書き込みフラグは Windows Vista 以降のバージョンの Windows で使用できます。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*

IRP を指定します\_MJ\_を記述します。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  

要求された操作を指定し、次のいずれかが含まれています。

-   IRP\_MN\_完了

-   IRP\_MN\_完了\_MDL

-   IRP\_MN\_完了\_MDL\_DPC

-   IRP\_MN\_圧縮

-   IRP\_MN\_DPC

-   IRP\_MN\_MDL

-   IRP\_MN\_MDL\_DPC

-   IRP\_MN\_標準

<a href="" id="irpsp--parameters-write-byteoffset"></a>*IrpSp-&gt;Parameters.Write.ByteOffset*  

大きな\_書き込まれるデータのファイル内の開始バイト オフセットを指定する整数変数です。

特定の状況でこのパラメーターに特殊な値が含まれます。 次に、例を示します。

-   次の条件が true の場合は、現在のファイルの末尾の明示的なファイルのオフセット値の代わりに使用することを示します。

    *IrpSp -&gt;Parameters.Write.ByteOffset.LowPart*ファイルを = =\_書き込み\_TO\_エンド\_の\_ファイルと*IrpSp-&gt;Parameters.Write.ByteOffset.HighPart* -1 を = =

<a href="" id="irpsp--parameters-write-key"></a>*IrpSp-&gt;Parameters.Write.Key*  

ターゲット ファイルのバイト範囲ロックに関連付けられているキーの値。

<a href="" id="irpsp--parameters-write-length"></a>*IrpSp-&gt;Parameters.Write.Length*  

書き込むデータのバイト長。 書き込まれたバイト数が返される、書き込み操作が成功した場合、**情報**、IO のメンバー\_状態\_によって示されるブロック構造*Irp-&gt;IoStatus*.

<a name="remarks"></a>注釈
-------

ファイル システムでは、書き込みを丸めるし、読み取り、基になるファイル ストレージ デバイスのセクター サイズの倍数で最大ファイルの最後に操作します。 読み取り前または前の書き込み操作を処理するときにフィルターを割り当てるし、スワップに関連付けられているデバイスのセクター サイズの倍数でまでの割り当てられたバッファーのサイズを丸めるバッファーが必要です。 一致しない場合、基になるファイル システムから転送されたデータの長さが割り当てられたバッファーの長さを超えています。 バッファーのスワップの詳細については、次を参照してください。 [swapBuffers ミニフィルター サンプル](https://go.microsoft.com/fwlink/p/?linkid=256055)します。

## <a name="see-also"></a>関連項目


[**CcMdlWriteComplete**](https://msdn.microsoft.com/library/windows/hardware/ff539172)

[**CcPrepareMdlWrite**](https://msdn.microsoft.com/library/windows/hardware/ff539181)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_READ**](irp-mj-read.md)

[**IRP\_MJ\_書き込み (WDK カーネル リファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)

[**ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile)

 

 







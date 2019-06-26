---
title: IRP_MJ_READ
description: IRP_MJ_READ
ms.assetid: f2f909ff-4af6-433e-9f3c-9692b5ab7171
keywords:
- IRP_MJ_READ インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_READ
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f5fd5ca30842163fd685b1305e977d2e754ad98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384811"
---
# <a name="irpmjread"></a>IRP\_MJ\_READ


## <a name="when-sent"></a>送信時


IRP\_MJ\_読み取り I/O マネージャーによって、またはファイル システム ドライバーによって要求が送信されます。 この要求を送信できますなど、ユーザー モード アプリケーションには、Microsoft Win32 関数が呼び出されるとなど**ReadFile**、カーネル モード コンポーネントが呼び出されたときまたは[ **ZwReadFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile).

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、パラメーターおよびマイナーの関数コードを確認するファイル オブジェクトをデコードする必要があります。

メモリ記述子のリスト (MDL) 要求を読み取り、ファイル システムは必要な操作を決定するマイナー関数コードを確認する必要があります。 次に、キャッシュされたファイルの I/O に対してのみ使用できる有効なマイナー関数コードを示します。

- IRP\_MN\_完了

- IRP\_MN\_完了\_MDL

- IRP\_MN\_完了\_MDL\_DPC

- IRP\_MN\_圧縮

- IRP\_MN\_DPC

- IRP\_MN\_MDL

- IRP\_MN\_MDL\_DPC

- IRP\_MN\_標準

この IRP の処理についての詳細については、Windows Driver Kit (WDK) で含まれている、CDFS および FASTFAT のサンプルを調べます。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、必要な処理を実行、フィルターの性質、によってすべて完了して、IRP が失敗するまたはかスタック上の次の下位ドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の読み取り要求の処理に IRP スタックの場所は、次のメンバーに含まれる情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  

ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  

システムが指定した場合に、中間システム バッファーとして使用するバッファーへのポインター、DO\_バッファーに格納された\_IO フラグに設定されて*デバイス オブジェクト -&gt;フラグ*。 このメンバーに設定している場合は、 **NULL**します。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  

ポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)最終的な完了の状態と、要求された操作に関する情報を受け取る。 詳細については、の説明を参照して、 *IoStatusBlock*パラメーターを[ **ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile)します。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  

読み取るデータを格納しているページを記述するメモリ記述子一覧 (MDL) のアドレス。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  

ファイルから読み取られるデータを受信する呼び出し元が指定の出力バッファーへのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  

関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。 場合、FO\_同期\_IO フラグに設定されて*IrpSp -&gt;FileObject -&gt;フラグ*、同期 I/O 用に、ファイル オブジェクトが開かれました。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_読み取り、使用する必要があります。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  

IRP を指定します\_MJ\_を読み取る。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  

要求された操作を指定し、次のいずれかが含まれています。

- IRP\_MN\_完了

- IRP\_MN\_完了\_MDL

- IRP\_MN\_完了\_MDL\_DPC

- IRP\_MN\_圧縮

- IRP\_MN\_DPC

- IRP\_MN\_MDL

- IRP\_MN\_MDL\_DPC

- IRP\_MN\_標準

<a href="" id="irpsp--parameters-read-byteoffset"></a>*IrpSp-&gt;Parameters.Read.ByteOffset*

大きな\_読み取られるデータのファイル内の開始のバイト オフセットを指定する整数型の変数。

<a href="" id="irpsp--parameters-read-key"></a>*IrpSp-&gt;Parameters.Read.Key*

ターゲット ファイルのバイト範囲ロックに関連付けられているキーの値。

<a href="" id="irpsp--parameters-read-length"></a>*IrpSp-&gt;Parameters.Read.Length*

読み取るデータのバイト長。 読み取られたバイト数が返される読み取り操作が成功した場合、**情報**のメンバー、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)によって示される構造*Irp -&gt;IoStatus*します。

<a name="remarks"></a>注釈
-------

ファイル システムでは、書き込みを丸めるし、読み取り、基になるファイル ストレージ デバイスのセクター サイズの倍数で最大ファイルの最後に操作します。 読み取り前または前の書き込み操作を処理するときにフィルターを割り当てるし、スワップに関連付けられているデバイスのセクター サイズの倍数でまでの割り当てられたバッファーのサイズを丸めるバッファーが必要です。 一致しない場合、基になるファイル システムから転送されたデータの長さが割り当てられたバッファーの長さを超えています。 バッファーのスワップの詳細については、次を参照してください。 [swapBuffers ミニフィルター サンプル](https://go.microsoft.com/fwlink/p/?linkid=256055)します。

## <a name="see-also"></a>関連項目


[**CcMdlRead**](https://docs.microsoft.com/previous-versions/ff539159(v=vs.85))

[**CcMdlReadComplete**](https://msdn.microsoft.com/library/windows/hardware/ff539163)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_読み取り (WDK カーネル リファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)

[**IRP\_MJ\_WRITE**](irp-mj-write.md)

[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile)

 

 







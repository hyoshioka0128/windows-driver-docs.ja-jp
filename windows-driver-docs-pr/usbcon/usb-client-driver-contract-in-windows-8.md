---
Description: このトピックでは、Windows 8 に含まれる USB ドライバースタックへの URB の割り当て、構築、および送信を行うためのクライアントドライバーのベストプラクティスについて説明します。
title: ベストプラクティス-URBs の使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3127c45b6e63e21e91c324152fcfff17db32b26a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843199"
---
# <a name="best-practices-using-urbs"></a>ベストプラクティス: URBs の使用


このトピックでは、Windows 8 に含まれる USB ドライバースタックへの URB の割り当て、構築、および送信を行うためのクライアントドライバーのベストプラクティスについて説明します。

Windows 8 には、ユニバーサルシリアルバス (USB) 3.0 デバイスをサポートする新しい USB ドライバースタックが含まれています。 新しい USB 3.0 ドライバースタックでは、USB 3.0 仕様に従って、いくつかの新機能が実装されています。 また、ドライバースタックには、クライアントドライバーが一般的なタスクを効率的に実行できるようにするその他の機能も含まれています。 たとえば、新しいドライバースタックでは、クライアントドライバーが、物理メモリ内の連続していないページで転送バッファーを送信できるようにするための、連鎖された MDLs を受け入れます。

クライアントドライバーは、Windows 8 用の USB ドライバースタックの新機能を使用できるようにするために、デバイス用に Windows によって読み込まれる、基になる USB ドライバースタックにドライバーを登録する必要があります。 クライアントドライバーを登録するには、 [**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)を呼び出し、*コントラクトのバージョン*を指定します。 クライアントドライバーが Windows 8 の機能強化と新機能をビルド、実行、および使用することを目的としている場合、クライアントコントラクトバージョンは USBD\_CLIENT\_CONTRACT\_VERSION\_602 です。

USBD\_クライアント\_コントラクト\_バージョン\_602 バージョンのクライアントドライバーの場合、USB ドライバースタックでは、クライアントドライバーが次の規則のセットに準拠していると想定しています。

-   [古いパイプハンドルまたは無効なパイプハンドルを使用して i/o 要求を送信しない](#do-not-send-io-requests-by-using-stale-or-invalid-pipe-handles)
-   [Windows 8 で割り当てルーチンを呼び出して URBs を割り当てる](#allocate-urbs-by-calling-allocation-routines-in-windows8)
-   [保留中の要求に関連付けられているアクティブな URBs を再利用しない](#do-not-reuse-active-urbs-associated-with-pending-requests)
-   [高速および SuperSpeed アイソクロナス転送には、8を超えるポーリング期間を使用しないでください。](#do-not-use-polling-period-greater-than-8-for-high-speed-and-superspeed-isochronous-transfers)
-   [フレームあたりのパケット数の倍数であるアイソクロナスパケットの数を確認します。](#make-sure-that-the-number-of-isochronous-packets-that-is-a-multiple-of-number-of-packets-per-frame)
-   [文書化された IRQL レベルでルーチンを呼び出します](#call-the-routine-at-the-documented-irql-level)
-   [関連トピック](#related-topics)

USB ドライバースタックは、受信した要求に対して検証を実行し、可能な限り違反を処理します。 そうしないと、未定義の動作が発生する可能性があります。

## <a name="do-not-send-io-requests-by-using-stale-or-invalid-pipe-handles"></a>古いパイプハンドルまたは無効なパイプハンドルを使用して i/o 要求を送信しない


クライアントドライバーは、古いパイプハンドルを使用して、USB ドライバースタックに i/o 要求を送信し*ない*ようにする必要があります。 *古いパイプハンドル*は、構成、インターフェイス、またはデバイスで選択されなくなった別の設定を選択するために要求で取得されたパイプハンドルを参照します。 古いパイプハンドルを回避するには、クライアントドライバーが構成またはインターフェイスを選択するたびに、ドライバーがパイプハンドルのキャッシュを更新する必要があります (通常はデバイスコンテキストに格納されます)。 競合状態によっては、パイプハンドルが古くなることもあります。 たとえば、クライアントドライバーは、選択したインターフェイスのパイプハンドルを使用して、i/o 要求を送信します。 要求が完了する前に、クライアントドライバーは、使用中のパイプハンドルに関連付けられているのと同じエンドポイントを使用しない代替設定を選択します。 これらの保留中の要求の両方で、パイプハンドルが無効になる競合状態が発生する可能性があります。

## <a name="allocate-urbs-by-calling-allocation-routines-in-windows8"></a>Windows 8 で割り当てルーチンを呼び出して URBs を割り当てる


Windows 8 には、USB 要求ブロック (URBs) を割り当て、ビルド、および解放するための新しいルーチンが用意されています。 URBs を割り当てるには、Windows Driver Model (WDM) クライアントドライバーが、次の一覧に示す新しいルーチンを常に使用する必要があります。

-   [**USBD\_Ur・検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)
-   [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)
-   [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)
-   [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)
-   [**USBD\_UrbFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree)
-   [**USBD\_割り当て Urbtoiostacklocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)

前の一覧のルーチンは、追跡と処理を改善するために、割り当てられた URB に不透明な URB コンテキストをアタッチする場合があります。 クライアントドライバーは、URB コンテキストの内容を表示または変更できません。 Windows 8 での URB 割り当ての詳細については、「 [URBs の割り当てとビルド](how-to-add-xrb-support-for-client-drivers.md)」を参照してください。

Windows Driver Framework (WDF) クライアントドライバーのバージョンを USBD\_CLIENT\_602\_\_CONTRACT として識別する場合 ( **WdfUsbTargetDeviceCreateWithParameters**を参照)、USB ドライバースタック新しい**WdfUsbTargetDeviceCreateUrb**を呼び出すことによって、クライアントドライバーが URB にメモリを割り当てることを想定しています。

## <a name="do-not-reuse-active-urbs-associated-with-pending-requests"></a>保留中の要求に関連付けられているアクティブな URBs を再利用しない


USB ドライバースタックは、URB に関連付けられている要求の前に再送信されたアクティブな URB を検出すると、意図的にバグチェックを行います。 要求が保留中であり、クライアントドライバーの IRP 完了ルーチンが呼び出されていない限り、URB はアクティブです。 アクティブな URB に対して次のタスクを実行しないでください。

-   別の要求に対してアクティブな URB を再送信しない (URB を別の IRP と関連付ける)*ことはできません*。
-   アクティブな URB の内容*を変更しないでください。*
-   アクティブな URB*を解放しないでください。*

クライアントドライバーの完了ルーチンが呼び出された後、ドライバーは、完了ルーチン内の特定の種類の要求に対して URBs を再送信できます。 再送信には、次の規則が適用されます。

-   クライアントドライバーは、 [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)によって割り当てられた URB を再利用しないでください。これは、選択構成要求以外の任意の種類の要求で同じ構成を選択する場合に使用します。
-   クライアントドライバーは、インターフェイスで同じ代替設定を選択するための選択インターフェイス要求以外の任意の種類の要求に対して、 [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)によって割り当てられた URB を再利用することはできません。 例については、「 **USBD\_SelectInterfaceUrbAllocateAndBuild**」の「解説」を参照してください。
-   [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)によって割り当てられた URB は、アイソクロナス転送要求に対してのみ再利用する必要があります。 逆に、他の種類の i/o 要求 (制御、一括、または割り込み) に割り当てられている URB は、アイソクロナス要求では使用できません。

    たとえば、クライアントドライバーは、一括転送要求の[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造を割り当てて構築します。 クライアントドライバーは、デバイス内のアイソクロナスエンドポイントにデータを送信することも必要になります。 一括転送要求の完了後、クライアントドライバーは、アイソクロナス要求の URB を再フォーマットして送信する*ことはできません*。 これは、アイソクロナス要求に関連付けられている URB が、パケットの数に応じて可変長であるためです。 また、パケットはフレーム境界で開始および終了する必要があります。 割り当てられた URB (一括転送用) が、アイソクロナス転送に必要なバッファーレイアウトに合わない可能性があり、要求が失敗する可能性があります。

-   [**USBD\_urに**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)よって割り当てられた URB は、アイソクロナス、選択構成、または選択インターフェイスの要求に再利用することはできません。 URB を再利用して、デバイスで選択した構成を無効にする NULL 構成を選択することができます。 URB がアクティブになっておらず、クライアントドライバーが[**Usbbuildselectconfigurationrequest**](https://docs.microsoft.com/previous-versions/ff538968(v=vs.85))マクロを呼び出し、 *CONFIGURATIONDESCRIPTOR*パラメーターに NULL を渡すことによって、urb を再フォーマットする必要があります。
-   クライアントドライバーは、URB を再送信する前に、要求の種類に対して定義された適切な**Usbbuildxxx**マクロを使用して、urb を再フォーマットする必要があります。 USB スタックによって内容の一部が変更されている可能性があるため、ドライバーで URB をフォーマットすることが重要です。

    たとえば、ドライバーが[**UsbBuildInterruptOrBulkTransferRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildinterruptorbulktransferrequest)を呼び出して一括転送要求の urb を初期化するとします (「 [ **\_urb\_bulk\_または\_INTERRUPT\_transfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_bulk_or_interrupt_transfer))」を参照してください。 ドライバーが[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体の**transferbuffermdl**メンバーを NULL に初期化した場合、USB ドライバースタックは、に指定された**転送バッファーを**使用して、データを MDL ではなくデバイスと交換します。 ただし、内部的には、USB ドライバースタックによって MDL が作成され、 **Transferbuffermdl**に mdl へのポインターが格納され、mdl を使用してデータがスタックに渡されることがあります。 USB ドライバースタックによって MDL メモリが解放されても、クライアントドライバーが完了ルーチンで URB を処理している場合、 **Transferbuffermdl**は NULL ではない可能性があります。 URB のメンバーが正しくフォーマットされていることを確認するには、ドライバーは**UsbBuildInterruptOrBulkTransferRequest**を再度呼び出して、要求を送信する前に urb を再フォーマットする必要があります。

## <a name="do-not-use-polling-period-greater-than-8-for-high-speed-and-superspeed-isochronous-transfers"></a>高速および SuperSpeed アイソクロナス転送には、8を超えるポーリング期間を使用しないでください。


USB ドライバースタックでは、ポーリング期間が1、2、4、または8の高速および SuperSpeed のアイソクロナスパイプがサポートされています。 クライアントドライバーは、期間が8より大きいエンドポイントに I/O を送信することはできません。 これを行うと、バグチェックが発生する可能性があります。

## <a name="make-sure-that-the-number-of-isochronous-packets-that-is-a-multiple-of-number-of-packets-per-frame"></a>フレームあたりのパケット数の倍数であるアイソクロナスパケットの数を確認します。


高速および SuperSpeed のアイソクロナス転送の場合、フレームあたりのアイソクロナスパケットの数は 8/ポーリング期間として計算されます。 クライアントドライバーは、URB に指定された**numberofpackets**値 (「 [ **\_urb\_ISOCH\_TRANSFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer)」を参照) がフレームあたりのパケット数の倍数であることを確認する必要があります。

USB ドライバースタックは、 **Numberofpackets**がフレームあたりのパケット数の倍数ではない場合に、アイソクロナス転送 URBs をサポートしていません。

## <a name="call-the-routine-at-the-documented-irql-level"></a>文書化された IRQL レベルでルーチンを呼び出します


クライアントドライバーを USBD\_クライアント\_\_コントラクトのバージョン\_602 に登録すると、クライアントドライバーは、クライアントドライバーが適切な IRQL レベルで要求を送信したと見なします。 クライアントドライバーがディスパッチ\_レベルで要求を送信する場合は、パッシブ\_レベルで送信される必要があります。 要求を受け取ったときに、USB ドライバースタックが IRQL 値を検証し、要求に失敗する場合があります。 ただし、それ以外の場合は、USB ドライバースタックによってバグチェックが生成されることがあります。

## <a name="related-topics"></a>関連トピック
[USB デバイスへの要求の送信](communicating-with-a-usb-device.md)  




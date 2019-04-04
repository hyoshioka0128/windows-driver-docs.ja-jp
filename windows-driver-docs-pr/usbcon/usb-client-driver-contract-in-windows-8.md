---
Description: This topic describes best practices for a client driver for allocating, building, and sending an URB to the USB driver stack included with Windows 8.
title: ベスト プラクティス - を使用して翻訳
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 496f0017819bfb9743948da82c41ae27eb91b235
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527987"
---
# <a name="best-practices-using-urbs"></a>ベスト プラクティス:翻訳を使用します。


このトピックでは、割り当て、構築、および Windows 8 に含まれている USB ドライバー スタックへ、URB の送信用のクライアント ドライバーのベスト プラクティスについて説明します。

Windows 8 には、ユニバーサル シリアル バス (USB) 3.0 デバイスをサポートする新しい USB ドライバー スタックが含まれています。 新しい USB 3.0 ドライバー スタックは、USB 3.0 の仕様に従って、いくつかの新機能を実装します。 さらに、ドライバー スタックには、一般的なタスクを効率的に実行するためのクライアント ドライバーを有効にするその他の機能が含まれています。 たとえば、新しいドライバー スタックは、チェーン-MDLs 隣接していないページの物理メモリ内転送バッファーを送信するクライアント ドライバーを許可するを受け入れます。

クライアント ドライバーは、Windows 8 USB ドライバー スタックの新機能を使用して、前に、ドライバーする必要がありますの登録には、デバイスが Windows によって読み込まれる基になる USB ドライバー スタック。 クライアント ドライバーを登録するには、呼び出す[ **USBD\_CreateHandle** ](https://msdn.microsoft.com/library/windows/hardware/hh406241)を指定し、*コントラクト バージョン*します。 クライアント ドライバーをビルド、実行、および Windows 8 の強化点と新機能を使用する場合は、クライアント コントラクト バージョンは USBD\_クライアント\_コントラクト\_バージョン\_602 します。

USBD の\_クライアント\_コントラクト\_バージョン\_クライアント ドライバーは、次の一連の規則に準拠するいると仮定 602 のバージョンのクライアント ドライバーを USB ドライバー スタック。

-   [古い場合または無効なパイプ ハンドルを使用して I/O 要求を送信できません。](#do-not-send-i-o-requests-by-using-stale-or-invalid-pipe-handles)
-   [Windows 8 の割り当てルーチンを呼び出すことで翻訳を割り当てる](#allocate-urbs-by-calling-allocation-routines-in-windows-8)
-   [保留中の要求に関連付けられているアクティブな翻訳を再利用しません。](#do-not-reuse-active-urbs-associated-with-pending-requests)
-   [高速および SuperSpeed isochronous 転送のポーリング期間が 8 より大きい値を使用しないでください。](#do-not-use-polling-period-greater-than-8-for-high-speed-and-superspeed-isochronous-transfers)
-   [必ずフレームあたりのパケットの数の倍数であるアイソクロナス パケットの数](#make-sure-that-the-number-of-isochronous-packets-that-is-a-multiple-of-number-of-packets-per-frame)
-   [文書化されている、IRQL レベル、ルーチンを呼び出す](#call-the-routine-at-the-documented-irql-level)
-   [関連トピック](#related-topics)

USB ドライバー スタックは、受信した要求の検証を実行し、可能であれば、違反を処理します。 そのためにはエラーは、未定義の動作に生じる可能性があります。

## <a name="do-not-send-io-requests-by-using-stale-or-invalid-pipe-handles"></a>古い場合または無効なパイプ ハンドルを使用して I/O 要求を送信できません。


クライアント ドライバーである必要があります*いない*古いパイプ ハンドルを使用して、USB ドライバー スタックに I/O 要求を送信します。 A*古いパイプ ハンドル*は、構成、インターフェイス、またはデバイスの選択を解除する代替の設定を選択する要求で取得したパイプ ハンドルを参照します。 古いパイプ ハンドルを避けるためには、クライアント ドライバーが、構成またはインターフェイスを選択するたびに、ドライバーは、(通常はデバイス コンテキストに格納されている)、パイプ ハンドルには、そのキャッシュを更新する必要があります。 特定の競合状態は、また、古いパイプ ハンドルがあります。 たとえば、クライアント ドライバーでは、パイプ ハンドルを選択したインターフェイスを使用して、I/O 要求を送信します。 要求が完了する前に、クライアント ドライバーは、使用中のパイプ ハンドルに関連付けられている同じエンドポイントを使用しない別の設定を選択します。 パイプ ハンドルが無効なため、競合状態、保留中の要求の両方があります。

## <a name="allocate-urbs-by-calling-allocation-routines-in-windows8"></a>Windows 8 の割り当てルーチンを呼び出すことで翻訳を割り当てる


Windows 8 は、割り当て、作成、および USB 要求のブロック (翻訳) を解放するための新しいルーチンを提供します。 翻訳を割り当てるには、Windows Driver Model (WDM) のクライアント ドライバーは常に次の一覧に表示される新しいルーチンを使用する必要があります。

-   [**USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)
-   [**USBD\_IsochUrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406231)
-   [**USBD\_SelectConfigUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406243)
-   [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406245)
-   [**USBD\_UrbFree**](https://msdn.microsoft.com/library/windows/hardware/hh406252)
-   [**USBD\_AssignUrbToIoStackLocation**](https://msdn.microsoft.com/library/windows/hardware/hh406228)

上記のルーチンは、追跡と処理を向上させるために割り当てられた URB を非透過の URB コンテキストをアタッチ可能性があります。 クライアント ドライバーでは、表示または URB コンテキストの内容を変更できません。 Windows 8 で URB 割り当ての詳細については、[割り当てと構成の翻訳](how-to-add-xrb-support-for-client-drivers.md)を参照してください。

場合 USBD とそのバージョンを識別する Windows Driver Framework (WDF) クライアント ドライバー\_クライアント\_コントラクト\_バージョン\_602 の登録時に (を参照してください**WdfUsbTargetDeviceCreateWithParameters**)、USB ドライバー スタックを呼び出して、新しい URB のメモリを割り当て、クライアント ドライバーが必要ですが**WdfUsbTargetDeviceCreateUrb**します。

## <a name="do-not-reuse-active-urbs-associated-with-pending-requests"></a>保留中の要求に関連付けられているアクティブな翻訳を再利用しません。


USB ドライバー スタックのバグチェックでは意図的に URB に関連付けられた、要求の前に再送信されました URB をアクティブなことが検出された場合。 要求が保留中であり、クライアント ドライバーの IRP の完了のルーチンが呼び出されていない限り、URB はアクティブです。 Active の URB では、次のタスクを行いません。

-   *いない*別の要求 (関連付け別の IRP で URB) の作業中の URB を再実行してください。
-   *いない*active の URB の内容を変更します。
-   *いない*active の URB を解放します。

クライアント ドライバーの完了のルーチンが呼び出された後、ドライバーは、特定の種類の要求完了ルーチン内での翻訳を再送信できます。 再送信の次の規則が適用されます。

-   クライアント ドライバーが割り当てられる、URB 再利用する必要があります[ **USBD\_SelectConfigUrbAllocateAndBuild** ](https://msdn.microsoft.com/library/windows/hardware/hh406243)同じを選択する select 構成要求以外の要求の種類にかかわらず構成します。
-   クライアント ドライバーが割り当てられる、URB 再利用する必要があります[ **USBD\_SelectInterfaceUrbAllocateAndBuild** ](https://msdn.microsoft.com/library/windows/hardware/hh406245)同じを選択する select インターフェイス要求以外の要求の種類にかかわらず代替インターフェイスで設定します。 例については、「解説」を参照してください。 **USBD\_SelectInterfaceUrbAllocateAndBuild**します。
-   割り当てられる、URB [ **USBD\_IsochUrbAllocate** ](https://msdn.microsoft.com/library/windows/hardware/hh406231)アイソクロナス転送要求に対してのみ再利用する必要があります。 逆に、他の種類の I/O 要求 (コントロールや一括、割り込み) に割り当てられた、URB が、アイソクロナス要求の使用はできません。

    たとえば、クライアント ドライバーの割り当て、ビルド、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)一括転送要求の構造体。 また、クライアント ドライバーは、デバイスのアイソクロナス エンドポイントにデータを送信したいと考えているとします。 クライアント ドライバーである必要がありますを一括転送要求が完了すると、*いない*再フォーマットし、URB アイソクロナス要求を送信します。 アイソクロナス、要求に関連付けられている、URB があるパケットの数によっては可変長であるためにです。 さらに、パケットは、開始および終了、フレームの境界線を必要があります。 (一括転送) の割り当てられた URB アイソクロナスの転送に必要なバッファー レイアウトに適合しないと、要求が失敗する可能性があります。

-   割り当てられる、URB [ **USBD\_UrbAllocate** ](https://msdn.microsoft.com/library/windows/hardware/hh406250)アイソクロナス、選択構成、または選択インターフェイス要求の再利用する必要があります。 URB は、デバイスで選択した構成を無効にする NULL 構成を選択するため再利用できます。 URB をアクティブにすることはできませんし、クライアント ドライバーは、呼び出すことによって、URB を再フォーマットする必要があります、 [ **UsbBuildSelectConfigurationRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538968)マクロとで NULL が渡される、 *ConfigurationDescriptor*パラメーター。
-   URB を再送信する前に、クライアント ドライバーは、適切なを使用して URB をフォーマットする必要があります**UsbBuildXxx**要求の種類に対して定義されているマクロ。 USB スタックの内容の一部変更がある可能性がありますので、ドライバー、URB を書式設定するために重要です。

    たとえば、ドライバーを呼び出す[ **UsbBuildInterruptOrBulkTransferRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538953) 、URB 一括転送要求の処理を初期化するために (を参照してください[  **\_URB\_一括\_または\_INTERRUPT\_転送**](https://msdn.microsoft.com/library/windows/hardware/ff540352))。 ドライバーが初期化する場合、 **TransferBufferMDL**のメンバー、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体を null の場合、USB ドライバー スタックは、指定した転送バッファーを使用して**TransferBuffer**MDL ではなく、デバイスとデータを交換します。 ただし、内部的には、USB ドライバー スタック、可能性があります、MDL の作成で MDL へのポインターを格納**TransferBufferMDL**MDL を使用して、スタックで、データを渡すとします。 USB ドライバー スタック MDL のメモリを解放する場合でも**TransferBufferMDL**クライアント ドライバーが完了ルーチンの URB を処理するときに、NULL をできない可能性があります。 URB のメンバーが正しく書式設定は、ドライバーを呼び出す必要があります**UsbBuildInterruptOrBulkTransferRequest** URB を要求を送信する前に再フォーマットするには、もう一度

## <a name="do-not-use-polling-period-greater-than-8-for-high-speed-and-superspeed-isochronous-transfers"></a>高速および SuperSpeed isochronous 転送のポーリング期間が 8 より大きい値を使用しないでください。


USB ドライバー スタックは、高速および SuperSpeed アイソクロナス パイプ 1、2、4、または 8 の場合は、ポーリング期間数をサポートします。 クライアント ドライバーでは、IO を 8 より大きい期間を持つエンドポイントに送信する必要があります。 これにより、バグチェックを生じる可能性があります。

## <a name="make-sure-that-the-number-of-isochronous-packets-that-is-a-multiple-of-number-of-packets-per-frame"></a>必ずフレームあたりのパケットの数の倍数であるアイソクロナス パケットの数


高速および SuperSpeed アイソクロナス転送は、フレームごとの isochronous パケットの数は 8/ポーリングの期間として計算されます。 クライアント ドライバーように注意してください、 **NumberOfPackets** URB で指定された値 (を参照してください[  **\_URB\_アイソクロナス\_転送**](https://msdn.microsoft.com/library/windows/hardware/ff540414)) フレームあたりのパケットの数の倍数です。

USB ドライバー スタックは、アイソクロナス転送の翻訳をサポートしていません、 **NumberOfPackets**フレームあたりのパケットの数の倍数ではありません。

## <a name="call-the-routine-at-the-documented-irql-level"></a>文書化されている、IRQL レベル、ルーチンを呼び出す


USBD をクライアント ドライバーを登録した場合\_クライアント\_コントラクト\_バージョン\_602 コントラクト バージョンとして、USB ドライバー スタックはこと、クライアント ドライバー要求を送信、適切な IRQL でレベル。 クライアント ドライバーでは、ディスパッチで要求を送信する場合\_レベルは、パッシブで送信する必要があります\_レベル。 場合によっては、要求を受信するとは、USB ドライバー スタックは、IRQL の値を検証し、要求は失敗します。 ただし、それ以外の場合、USB ドライバー スタックでのバグチェックを生成可能性があります。

## <a name="related-topics"></a>関連トピック
[USB デバイスに要求を送信](communicating-with-a-usb-device.md)  




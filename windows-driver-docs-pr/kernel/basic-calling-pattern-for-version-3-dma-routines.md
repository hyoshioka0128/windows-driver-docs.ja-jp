---
title: バージョン 3 の DMA ルーチンの基本的な呼び出しパターン
description: DMA 操作のインターフェイスのバージョン 3 で、ルーチンを使用する DMA 転送を実行するには、ドライバーは、次の一覧で説明されている手順に従う必要があります。
ms.assetid: 5D73120F-79F5-4C9A-8AE5-25D5CF9B06F5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4388b99b25791bd7440c3e611f65d375f4de6f29
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326046"
---
# <a name="basic-calling-pattern-for-version-3-dma-routines"></a>バージョン 3 の DMA ルーチンの基本的な呼び出しパターン


DMA 操作のインターフェイスのバージョン 3 で、ルーチンを使用する DMA 転送を実行するには、ドライバーは、次の一覧で説明されている手順に従う必要があります。 次の手順では、下位のデバイスとバス マスターのデバイスの両方に共通です。 このインターフェイスのバージョン 3 では、Windows 8 以降で使用できます。 このインターフェイスでルーチンの詳細については、次を参照してください。 [ **DMA\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544071)します。

## <a name="step-1-obtain-a-dma-adapter-object"></a>手順 1:DMA アダプター オブジェクトを取得します。


DMA 転送の準備として、ドライバーが呼び出す、 [ **IoGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff549220)ルーチン DMA アダプター オブジェクトを取得します。 DMA のアダプター オブジェクトは、バス マスター デバイス、またはシステム DMA コント ローラーの要求行のいずれかを表すソフトウェア オブジェクトです。 このオブジェクトには、デバイス間でデータを転送するために使用するバスの DMA 操作のインターフェイスが含まれています。 さらに、このオブジェクトは、転送を実行するために必要な共有リソースへのドライバーのアクセスを同期します。 詳細については、次を参照してください。[アダプター オブジェクトの概要](introduction-to-adapter-objects.md)します。

## <a name="step-2-obtain-a-description-of-the-required-dma-resources"></a>手順 2:DMA の必要なリソースの説明を取得します。


ドライバーの呼び出し、 [ **GetDmaTransferInfo** ](https://msdn.microsoft.com/library/windows/hardware/hh451125)ルーチンを転送を実行する必要がある DMA リソースの説明を取得します。

この呼び出しの入力パラメーターには、転送、および転送の方向 (読み取りまたは書き込み) を使用するメモリ バッファーについて説明します。

この呼び出しから取得したリソースの要件には、マップのレジスタの数と、転送データのバッファーを記述するために必要なスキャッター/ギャザー リストのサイズが含まれます。 以降の呼び出しで、 [ **AllocateAdapterChannelEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406340)ルーチン (を参照してください[3.](#step-3-request-the-required-dma-resources))、ドライバーは、入力パラメーターとしてマップ登録数を提供します。

## <a name="step-3-request-the-required-dma-resources"></a>手順 3:DMA の必要なリソースを要求します。


ドライバーの呼び出し、 [ **AllocateAdapterChannelEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406340)ルーチン DMA のアダプター オブジェクトに割り当てるリソースを割り当てます。 これらのリソースは、DMA チャネルを含めるし、レジスタにマップします。

**AllocateAdapterChannelEx**呼び出しは非同期または同期することができます。

場合、DMA\_同期\_コールバック フラグが設定されていない、呼び出しは非同期です。 ここで、 *ExecutionRoutine*パラメーターは、要求されたリソースが使用可能なときに呼び出される呼び出し元が指定した実行ルーチンを指します。 成功した場合、非同期**AllocateAdapterChannelEx**呼び出しのステータスを返します\_実行ルーチンに実行を待機することがなく成功します。

場合、DMA\_同期\_コールバック フラグが設定されて、 **AllocateAdapterChannelEx**呼び出しは同期的です。 ここで、 *ExecutionRoutine*呼び出しのパラメーターは省略可能でと**AllocateAdapterChannelEx**ように動作します。

-   場合*ExecutionRoutine* NULL 以外の場合は、DMA リソースは、すぐに割り当てることができると**AllocateAdapterChannelEx**呼び出し元のスレッドのコンテキストで実行ルーチンを呼び出します。 実行のルーチンの実行が完了したら**AllocateAdapterChannelEx**ステータスを返します\_成功します。 リソースをすぐに利用しない場合は**AllocateAdapterChannelEx**が失敗し、エラー ステータス コードの状態を返します\_不十分\_リソース。

-   場合*ExecutionRoutine*が null の場合、および**AllocateAdapterChannelEx** DMA のリソースを割り当てることがすぐに**AllocateAdapterChannelEx** のステータスを返します\_成功します。 呼び出しがエラー状態コードの状態が失敗したすべてのリソースがすぐに利用できない場合は、\_不十分\_リソース。

状態を返す同期呼び出し\_成功すると場合、 *MapRegisterBase*パラメーターを**AllocateAdapterChannelEx** NULL 以外の場合は、 **AllocateAdapterChannelEx**によって示されるアドレスに割り当てられたマップのベース アドレスを登録の書き込み、 *MapRegisterBase*パラメーター。 場合*ExecutionRoutine*が null の場合、 *MapRegisterBase* NULL 以外である必要があります。 場合*ExecutionRoutine* NULL 以外の場合は、 *MapRegisterBase*パラメーターを**AllocateAdapterChannelEx**オプションですが、実行ルーチンが、マップのレジスタを送受信入力パラメーターとしてベース アドレス。

非同期**AllocateAdapterChannelEx**呼び出し、 *ExecutionRoutine* NULL 以外の場合があります。 実行ルーチンが、入力パラメーターとしてマップ レジスタのベース アドレスを受け取るとします。

後続の呼び出しで、 [ **MapTransferEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406521)ルーチン (を参照してください[手順 5](#step-5-initialize-the-dma-resources-and-start-the-dma-transfer))、ドライバーは、入力パラメーターとしてマップ レジスタのベース アドレスを指定します。

場合*ExecutionRoutine*が NULL 以外の場合、実行ルーチンが割り当てられているリソースのディス ポジションを示すステータス値を返します。 システム DMA 転送では、この戻り値がある必要があります**KeepObject**します。 この値は、オペレーティング システムは使用して、解放しないでアダプター オブジェクト (およびその割り当てられたリソースのすべて) を通知します。 ドライバーが代わりに呼び出す必要があります実行ルーチンが指定されていない場合、 [ **FreeAdapterObject** ](https://msdn.microsoft.com/library/windows/hardware/hh451107)ルーチンと供給**KeepObject**として、 *AllocationOption*パラメーター。

## <a name="step-4-if-necessary-cancel-the-pending-resource-request"></a>手順 4:必要に応じて、保留中のリソースの要求を取り消し


後に、 **AllocateAdapterChannelEx** 、DMA アダプター ドライバー、DMA のリソースを待機することができます、キューを呼び出すために必要な場合、呼び出し、 [ **CancelAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/hh406374)ルーチンを保留中のリソース要求を取り消します。

場合**CancelAdapterChannel**リソース要求が正常に取り消された TRUE が返されます。 実行ルーチンが指定された場合、 **AllocateAdapterChannelEx**呼び出し、このルーチンは実行されません。

場合**CancelAdapterChannel**既に付与されているために、リソース要求をキャンセルできません FALSE が返されます。 実行ルーチンが指定された場合、 **AllocateAdapterChannelEx**呼び出し、このルーチンが呼び出されます。

## <a name="step-5-initialize-the-dma-resources-and-start-the-dma-transfer"></a>手順 5:DMA リソースの初期化し、DMA の転送を開始


ドライバー呼び出し[ **MapTransferEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406521) DMA 転送を開始して DMA のリソースを初期化します。 この呼び出しを呼び出すのと同じドライバー スレッドで発生した**AllocateAdapterChannelEx**に、ドライバーが提供する実行ルーチンで発生した、または**AllocateAdapterChannelEx**します。 1 つ以上の場合**MapTransferEx** DMA データ バッファー全体を転送する呼び出しが必要です、後で**MapTransferEx**以前完了ルーチンで発生した呼び出し**MapTransferEx**呼び出します。

**MapTransferEx**サポートには、入力パラメーターとして MDLs がチェーンされています。 各 MDL では、仮想メモリ内で連続している DMA バッファーの領域について説明します。 ときに**MapTransferEx**スキャッター/ギャザー リストで、ドライバーの介入なしに仮想的に連続するバッファーの 1 つのリージョンからの移行を自動的に処理します。 詳細については、次を参照してください。 [MapTransferEx ルーチンを使用して](using-the-maptransferex-routine.md)します。

DMA 転送システムの場合に、DMA 完了ルーチンへのポインターを渡すことが**MapTransferEx** 、省略可能な*DmaCompletionRoutine*パラメーター。 このルーチンは、DMA 転送が完了したことを示すシステム DMA コント ローラーから、割り込みに応答でディスパッチで実行する予定です。

場合**MapTransferEx**が要求された転送の全体サイズをマップすることができません、設定されます、 \**長さ*出力マップされた長さのパラメーターとリターン状態\_成功しました。

## <a name="step-6-if-necessary-perform-hardware-specific-operations"></a>手順 6:必要に応じて、ハードウェア固有の操作を実行します。


**MapTransferEx**ステータスを返します\_DMA 転送が正常に開始されたことを示す成功します。 一部のプラットフォームで、ドライバーは、外側のいくつかの追加アクションを実行する必要があります、 **MapTransferEx**転送を開始する、呼び出しが遅延起動のこの型はすべてのプラットフォームで必要ありません。 ドライバーは、このような遅延を使用して、割り当てられたリソースを解放することについての決定のために依存する必要があります。

DMA 操作のインターフェイスのルーチンでは、これらのルーチンを使用するドライバーに対して透過的な方法では、DMA 転送のキャッシュの一貫性を維持します。 ハードウェア、キャッシュの一貫性を強制しないプラットフォームで**MapTransferEx**により、プロセッサのデータ キャッシュは、書き込み (メモリ デバイス) を転送する前にフラッシュされます。 呼び出し中に、読み取り (デバイスのメモリ) の転送に、キャッシュが無効になる、 [ **FlushAdapterBuffersEx** ](https://msdn.microsoft.com/library/windows/hardware/hh451102)ルーチン (を参照してください[手順 8](#step-8-flush-any-data-that-remains-in-the-cache)) すべて続く**MapTransferEx**呼び出します。

## <a name="step-7-receive-notification-when-the-dma-transfer-finishes"></a>手順 7:DMA 転送が完了すると、通知を受け取る


DMA 転送が完了したら、これら 2 つの方法のいずれかでドライバーが通知されます。

-   デバイス ドライバー、バス マスターのデバイスに、割り込み
-   システムの DMA コント ローラーを使用する下位のデバイスのドライバーによって提供される完了ルーチンの実行

DMA 転送システムは、ドライバーは完了ルーチンを指定できます**MapTransferEx**入力パラメーターとして。
## <a name="step-8-flush-any-data-that-remains-in-the-cache"></a>手順 8:キャッシュに残っているすべてのデータをフラッシュします。


DMA 転送が完了すると、ドライバーを呼び出す必要があります、 [ **FlushAdapterBuffersEx** ](https://msdn.microsoft.com/library/windows/hardware/hh451102)ルーチンをキャッシュに残っているすべてのデータをフラッシュします。 ドライバーを呼び出す必要があります**FlushAdapterBuffersEx**後すべて**MapTransferEx**呼び出します。

場合、 **MapTransferEx**呼び出し DMA データ バッファーの一部のみをマップすると、ドライバーを呼び出す必要があります**MapTransferEx**残りのデータをマップするには、もう一度です。 複雑な転送には、いくつか必要があります**MapTransferEx**呼び出し。 各追加**MapTransferEx**呼び出し、手順 5 ~ 8 を繰り返します。

## <a name="step-9-free-the-dma-channel-and-map-registers"></a>手順 9:DMA チャネルを解放し、マップを登録します


DMA データ バッファー全体が正常にマップすると、最終的な転送が完了すると、ドライバーを呼び出す必要があります、 [ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff549101) DMA チャネルとそのすべてを解放するルーチンに割り当てたマップ登録します。

## <a name="step-10-release-the-dma-adapter-object"></a>手順 10:DMA アダプター オブジェクトを解放します。


DMA のすべての転送が完了し、以前に割り当てられたマップ レジスタが解放される、ドライバーを呼び出す、 [ **PutDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff559965)ルーチン アダプター オブジェクトを解放します。

 

 





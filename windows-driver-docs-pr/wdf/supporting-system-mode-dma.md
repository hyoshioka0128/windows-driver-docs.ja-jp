---
title: システム モード DMA をサポートしています。
description: KMDF ドライバーがそのイベントに提供するコードを記述システム モード DMA のデバイスの I/O 要求を処理するコールバック関数。
ms.assetid: CCC77C15-69CA-44CB-8DEB-29F3EAEA44F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d629648ae39ec68f5817d8f58fbda8ff75e685c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557831"
---
# <a name="supporting-system-mode-dma"></a>システム モード DMA をサポートしています。


\[KMDF にのみ適用されます。\]

対照的に、システム モード DMA*バス マスター* DMA では、複数のデバイスが、通常、マルチ チャネルの 1 つの DMA コント ローラーを共有する構成を説明します。

カーネル モード ドライバー フレームワーク (KMDF) バージョン 1.11 以降は、フレームワークがサポートするシステム モードの DMA チップ (SoC) のシステムに – ベースの Windows 8 または Windows オペレーティング システムの以降のバージョンで実行されているシステム。

このトピックでは、KMDF ドライバーは、そのイベントのコールバック関数や、登録する省略可能なイベント コールバック関数で提供する必要があるコードを説明しますシステム モード DMA のデバイスの I/O 要求を処理します。

KMDF とバス マスター DMA については、[KMDF ドライバーでは、バス マスター DMA デバイスの I/O 要求の処理](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)を参照してください。

次の図は、イベントには、ドライバーはサポート システム モードの DMA を使用してコールバック関数を示します。

![kmdf ドライバーでのシステム モード dma の実装](images/sys-mode-dma-in-kmdf.png)

## <a name="creating-a-system-mode-dma-enabler"></a>システム モードの DMA イネーブラーを作成します。


2 段階のプロセスは、システム モード DMA プロファイルを作成します。 次の手順では、一般的なシナリオを表します。

1.  では通常、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数では、ドライバー呼び出し[ **WDF\_DMA\_イネーブラー\_CONFIG\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff551292)で、設定、**プロファイル**パラメーターを**SystemMode**または**SystemModeDuplex**します。 ドライバーを呼び出して[ **WdfDmaEnablerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff546983)を渡して、 [ **WDF\_DMA\_イネーブラー\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551290)受信したことを構造体します。

    ドライバー イネーブラー中に作成または[ *EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)します。

2.  ドライバーの[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数は、呼び出すことによって、DMA リソースを DMA イネーブラーを関連付けます、 [ **WdfDmaEnablerConfigureSystemProfile** ](https://msdn.microsoft.com/library/windows/hardware/hh451108)メソッド。 ドライバーの呼び出しを双方向のイネーブラー [ **WdfDmaEnablerConfigureSystemProfile** ](https://msdn.microsoft.com/library/windows/hardware/hh451108) 2 回、各転送の方向を構成する 1 回です。

    ドライバーが呼び出せる[ **WdfDmaEnablerConfigureSystemProfile** ](https://msdn.microsoft.com/library/windows/hardware/hh451108)後[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)が完了したらが、ドライバーは、DMA のトランザクションを初期化する前に、このメソッドを呼び出す必要があります。

## <a name="providing-optional-callback-functions"></a>省略可能なコールバック関数を提供します。


### <a href="" id="configuring-a-system-mode-dma-enabler"></a>DMA チャネルを構成します。

通常、KMDF ドライバーでは、DMA チャネルは構成しないでください。 ただし、特定の状況では、ドライバーはチャネル固有の構成を実行する必要があります。 たとえば、ドライバーでは、DMA コント ローラーで、次の手順を使用して実装されているカスタム関数を呼び出すことができます。

1.  ドライバーのいずれかで[要求ハンドラー](request-handlers.md)、ドライバー呼び出し[ **WdfDmaTransactionSetChannelConfigurationCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh451184)を登録する、 [ *EvtDmaTransactionConfigureDmaChannel* ](https://msdn.microsoft.com/library/windows/hardware/hh406414)コールバック関数。
2.  ドライバーの[ *EvtDmaTransactionConfigureDmaChannel* ](https://msdn.microsoft.com/library/windows/hardware/hh406414)コールバック関数の呼び出し[ **WdfDmaEnablerWdmGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff547020)にWDM へのポインターを取得[ **DMA\_アダプター**](https://msdn.microsoft.com/library/windows/hardware/ff544062)します。 この構造体は、ドライバーのシステム モード DMA チャネルを表すアダプター オブジェクトです。
3.  ドライバーを呼び出して[ **ConfigureAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/hh450939) DMA コント ローラーによって実装されるカスタム関数を有効にします。 このルーチンはで返されるアドレスからポインターによってのみ呼び出し可能な[ **DMA\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544071)構造体。
4.  ドライバーの[ *EvtDmaTransactionConfigureDmaChannel* ](https://msdn.microsoft.com/library/windows/hardware/hh406414)コールバック関数は、DMA チャネルを正常に構成した場合に TRUE を返します。
5.  フレームワークは、ドライバーの[ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)コールバック関数。

### <a name="receiving-notification-of-transfer-completion"></a>転送完了の通知を受信

をバス マスターのコント ローラーを使用するデバイスとは異なりシステム モード DMA デバイスのハードウェアは、割り込みを発行して DMA 転送の完了を通知可能性があります。

デバイスは DMA 転送の完了を通知する割り込みが発生しない場合、ドライバーを提供できます、 [ *EvtDmaTransactionDmaTransferComplete* ](https://msdn.microsoft.com/library/windows/hardware/hh406418)ときにフレームワークから呼び出されるイベント コールバック関数システム モード DMA の転送が完了しました。

このコールバック関数を登録するドライバーを呼び出す[ **WdfDmaTransactionSetTransferCompleteCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh439261)のいずれかからその[要求ハンドラー](request-handlers.md)。

 

 






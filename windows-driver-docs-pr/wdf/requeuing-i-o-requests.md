---
title: I/O 要求をキューに戻す
description: I/O 要求をキューに戻す
ms.assetid: b509959c-b2ab-4f04-9c08-5c5e90726b73
keywords:
- I/o 要求 WDK KMDF、キュー
- キュー i/o 要求 (WDK KMDF)
- 要求処理 WDK KMDF、キュー i/o 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bb0fa03d0925faa5fa066d3ed05787926b42755
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842222"
---
# <a name="requeuing-io-requests"></a>I/O 要求をキューに戻す





ドライバーは、i/o キューから取得した i/o 要求をキューへできます。 ドライバーが同じデバイス用に作成した別の i/o キューに i/o 要求をキューへことができます。 さらに、[バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)は、子デバイスの i/o キューから親デバイスの i/o キューに i/o 要求をキューへことができます。

### <a name="requeuing-an-io-request-to-a-different-io-queue-for-a-device"></a>デバイスの別の i/o キューに i/o 要求をキュー

ドライバーの要求ハンドラーがドライバーの i/o キューから i/o 要求を受信すると、ドライバーは[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)を呼び出して、要求を別のキューにキューへことができます。

たとえば、ドライバーが要求を処理する前に要求にリソースを割り当てる場合、ドライバーの[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)コールバック関数は、すべての要求を受信し、各要求のコンテキストメモリにリソース情報を格納した後、を呼び出すことができます。[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue) 。各要求を追加のキューにキューへします。

ドライバーが[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)を呼び出して、ドライバーが順次[ディスパッチ方法](dispatching-methods-for-i-o-requests.md)を使用している i/o キューから取得した i/o 要求をキューへする場合、フレームワークは次の i/o 要求をシーケンシャルキューからに送信します。キューの要求が完了するのを待たずにドライバーが必要です。

ドライバーが手動ディスパッチメソッドを使用している場合は、 [**WdfRequestRequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestrequeue)メソッドを呼び出して、ドライバーが取得した i/o キューの先頭に i/o 要求を返すことができます。 **WdfRequestRequeue**を呼び出すと、ドライバーの次の[**WdfIoQueueRetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)の呼び出しで、キューの要求が取得されます。

### <a name="requeuing-an-io-request-to-a-parent-devices-io-queue"></a>キューは、親デバイスの i/o キューに i/o 要求を

親デバイスの関数ドライバーは、親デバイスの子デバイスを[列挙](enumerating-the-devices-on-a-bus.md)し、子デバイスの[物理デバイスオブジェクト](wdm-concepts-for-kmdf-drivers.md#device-stacks)(pdos) を作成する[バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)として機能することができます。 このようなドライバーでは、親デバイスが処理する必要がある子デバイスの i/o 要求を受け取ることがあります。

たとえば、プロトコルバス (USB など) では、通常、接続されている各デバイスに割り当てられているハードウェアリソースが制御されます。 したがって、通常、親バスの関数ドライバーは、各子デバイスの i/o 操作を処理します。 I/o マネージャーが、子デバイスの1つの[デバイススタック](wdm-concepts-for-kmdf-drivers.md#device-stacks)に i/o 要求を送信すると、そのドライバーが子デバイスの PDO を作成したため、そのドライブのいずれかの子デバイスの i/o キューで i/o 要求を受信します。 ドライバーが親バスデバイスのコンテキストで i/o 要求を処理できるようにするには、その前に、子デバイスの i/o キューから親デバイスに属する i/o キューに i/o 要求をキューへする必要があります。

ただし、ドライバーは[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)を呼び出して、子のキューから親のキューに要求を移動することはできません。 I/o マネージャーは親デバイスと子デバイス用に個別のデバイススタックを作成するため、基になる WDM デバイスオブジェクトを、最初に子デバイスを表すものから親を表すものに変更する必要があります。

KMDF のバージョン1.9 より前では、ドライバーは、[リモート i/o ターゲット](general-i-o-targets.md)を作成し、子デバイスのデバイススタックのサイズを増やし、正しい WDM デバイスオブジェクトを指定することによってのみ、子デバイスから親に i/o 要求を送信できました。

KMDF バージョン1.9 以降では、ドライバーは子デバイスを作成する前に[**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent)を呼び出し、 [**WdfRequestForwardToParentDeviceIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)を呼び出して、子の i/o キューから親に要求をキューへできます。再生. ドライバーで**WdfPdoInitAllowForwardingRequestToParent**と**WdfRequestForwardToParentDeviceIoQueue**が使用されている場合、フレームワークは子のデバイススタックサイズを増やし、正しい WDM デバイスオブジェクトを i/o 要求に割り当てます。

 

 






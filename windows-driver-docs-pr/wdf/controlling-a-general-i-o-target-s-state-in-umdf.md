---
title: UMDF での一般 I/O ターゲットの状態の制御
description: UMDF での一般 I/O ターゲットの状態の制御
ms.assetid: 479487b2-5ce5-4522-b195-58ee50d210b6
keywords:
- '一般的な i/o ターゲット: WDK UMDF、状態'
- i/o ターゲット状態 WDK UMDF を開始しました
- 停止した i/o ターゲット状態 WDK UMDF
- クエリの終了-状態 WDK UMDF の削除
- 閉じた i/o ターゲット状態 WDK UMDF
- 削除された i/o ターゲット状態 WDK UMDF
- ローカル i/o ターゲット (WDK UMDF)
- リモート i/o ターゲット (WDK UMDF)
- i/o ターゲットの停止
- i/o ターゲットの再起動
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f51efc9445a154592db73216cc495b858565f1e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843644"
---
# <a name="controlling-a-general-io-targets-state-in-umdf"></a>UMDF での一般 I/O ターゲットの状態の制御


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは、一般的な i/o ターゲットに対して次の状態を定義します。

<a href="" id="started"></a>**開始**  
I/o ターゲットが開いている (つまり、UMDF ドライバーによって使用可能になっている) と、ドライバーは i/o ターゲットに i/o 要求を送信できます。 フレームワークは、適切なドライバーに要求を配信します。

<a href="" id="stopped"></a>**なく**  
I/o ターゲットは開かれていますが、 [**IWDFIoRequest:: send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出すと、ドライバーが WDF\_\_要求を渡し、\_オプションを送信して、\_ターゲット\_状態フラグを\_*フラグ*パラメーターに渡すことができない限り、i/o ターゲットに i/o 要求を送信することはできません。

フレームワークは、適切なドライバーへの要求の配信を停止します。

<a href="" id="closed-for-query-remove-------"></a>**クエリの終了-  の削除**  
I/o ターゲットは、デバイスがすぐに削除される可能性があるため、一時的に閉じられています。

<a href="" id="closed"></a>**開閉**  
I/o ターゲットは閉じているため、開始または停止できません。

<a href="" id="deleted"></a>**削除**  
I/o ターゲットのデバイスは削除されています。

[**WDF\_IO\_ターゲット\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)列挙体は、これらの状態を表す値を定義します。

### <a name="local-io-target-states"></a>ローカル i/o ターゲットの状態

フレームワークによって、ローカルの i/o ターゲットが自動的に開き、開始されます。

必要に応じて、ドライバーは[**IWDFIoTargetStateManagement:: Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)を呼び出してローカル i/o ターゲットを一時的に停止し、 [**IWDFIoTargetStateManagement:: Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)を呼び出して再起動することができます。 たとえば、ドライバーは、一時的なエラー状態を検出し、エラー状態が修正された場合に i/o ターゲットを再起動すると、ローカル i/o ターゲットを停止することがあります。

ローカル i/o ターゲットのデバイスが削除されると、フレームワークは自動的に i/o ターゲットを停止して閉じ、ターゲットのキューにあるすべての i/o 要求を[キャンセル](canceling-i-o-requests.md)します。 フレームワークは、デバイスオブジェクトイベントコールバック関数を呼び出すことによって、デバイスが使用できなくなったことをドライバーに通知します。 これらのコールバック関数の詳細については、「 [UMDF の PnP および電源管理のシナリオ](pnp-and-power-management-scenarios-in-umdf.md)」を参照してください。

ドライバーは[**IWDFIoTargetStateManagement:: GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)を呼び出して、ローカル i/o ターゲットの現在の状態を取得できます。

### <a name="remote-io-target-states"></a>リモート i/o ターゲットの状態

ドライバーは、 [**Iwdfremotetarget:: OpenFileByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)または[**Iwdfremotetarget:: openremoteinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface)を呼び出して、リモート i/o ターゲットを開く必要があります。 ドライバーがリモート i/o ターゲットを開くと、フレームワークは i/o ターゲットを自動的に開始します。

必要に応じて、ドライバーは[**Iwdfremotetarget:: Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-stop)を呼び出して、リモート i/o ターゲットを一時的に停止し、 [**Iwdfremotetarget:: Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-start)を呼び出して再起動することができます。

リモート i/o ターゲットのデバイスが削除されると、フレームワークは自動的に i/o ターゲットを停止して閉じ、次のイベントコールバック関数をドライバーが登録しない限り、ターゲットのキューにあるすべての i/o 要求をキャンセルします。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetqueryremove--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetQueryRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetqueryremove)  
リモート i/o ターゲットのデバイスが削除される可能性があることをドライバーに通知します。 ドライバーがデバイスの削除を許可する場合は、ドライバーが[**Iwdfremotetarget:: CloseForQueryRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-closeforqueryremove)を呼び出す必要があります。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetremovecomplete--------"></a>[**IremotetargetOnRemoteTargetRemoveComplete の削除::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetremovecomplete)  
リモート i/o ターゲットのデバイスが削除されたことをドライバーに通知します。 このコールバック関数は、 [**Iwdfremotetarget:: Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-close)を呼び出す必要があります。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetremovecanceled--------"></a>[**IremotetargetOnRemoteTargetRemoveCanceled の削除::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetremovecanceled)  
リモート i/o ターゲットのデバイスを削除しようとしたことがキャンセルされたことをドライバーに通知します。 ドライバーがターゲットを引き続き使用するようにするには、ドライバーが[**Iwdfremotetarget:: 再度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-reopen)を呼び出す必要があります。 通常、ドライバーは**OnRemoteTargetRemoveCanceled**コールバック関数内から**再び開く**ことを呼び出しますが、 **OnRemoteTargetRemoveCanceled**が返された後で、**再度開く**ことができます。

ドライバーは、 [**Iwdfremotetarget:: GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-getstate)を呼び出して、リモート i/o ターゲットの現在の状態を取得できます。

 

 






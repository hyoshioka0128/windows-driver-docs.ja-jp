---
title: UMDF での一般 I/O ターゲットの状態の制御
description: UMDF での一般 I/O ターゲットの状態の制御
ms.assetid: 479487b2-5ce5-4522-b195-58ee50d210b6
keywords:
- 一般的な I/O WDK UMDF、状態をターゲットします。
- 対象の状態の I/O WDK UMDF の開始
- 対象の状態の I/O WDK UMDF を停止しました
- クエリの削除状態 WDK UMDF の終了
- 終了した I/O ターゲット状態 WDK UMDF
- 削除された I/O ターゲット状態 WDK UMDF
- ローカルの I/O ターゲット WDK UMDF
- リモートの I/O ターゲット WDK UMDF
- I/O ターゲットを停止しています
- I/O ターゲットを再起動します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d1368de4df4f2f559e3405dc901d6c4ead9e474
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382877"
---
# <a name="controlling-a-general-io-targets-state-in-umdf"></a>UMDF での一般 I/O ターゲットの状態の制御


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークには、次の状態の一般的な I/O ターゲットを定義します。

<a href="" id="started"></a>**開始**  
I/O ターゲットが開いている (つまり、UMDF ドライバーを使用可能な) と、ドライバーに I/O 要求を送信することができます。 フレームワークは、適切なドライバーを要求を配信します。

<a href="" id="stopped"></a>**停止**  
UMDF ドライバーは、ドライバーは、WDF を通過しない限りに、I/O ターゲットへの I/O 要求を送信できない場合は I/O ターゲットが開いて、\_要求\_送信\_オプション\_無視\_ターゲット\_状態フラグ*フラグ*への呼び出しでパラメーター、 [ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッド。

フレームワークは、適切なドライバーへの要求の配信を停止します。

<a href="" id="closed-for-query-remove-------"></a>**クエリの削除の終了**   
I/O ターゲットは、そのデバイスを削除できるだけ可能性がありますのでは一時的に閉じられます。

<a href="" id="closed"></a>**終了**  
I/O ターゲットが閉じられると、開始または停止することはできません。

<a href="" id="deleted"></a>**削除**  
I/O ターゲットのデバイスが削除されました。

[ **WDF\_IO\_ターゲット\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)列挙は、これらの状態を表す値を定義します。

### <a name="local-io-target-states"></a>ローカル I/O ターゲットの状態

フレームワークは自動的に開き、ローカルの I/O ターゲットを起動します。

かどうか、必要に応じて、ドライバーを呼び出して[ **IWDFIoTargetStateManagement::Stop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)ローカルのターゲットの I/O および呼び出しを一時的に停止する[ **IWDFIoTargetStateManagement::Start** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)を再起動します。 たとえば、ドライバーは、一時的なエラー条件を検出した場合は、ローカル I/O ターゲットを停止し、エラー状態が修正された場合に I/O ターゲットを再起動することが。

フレームワークが自動的に停止し、I/O ターゲットを閉じる場合は、ローカルの I/O 対象のデバイスを削除すると、および[キャンセル](canceling-i-o-requests.md)ターゲットのキューにあるすべての I/O 要求。 フレームワークは、デバイス オブジェクトのイベントのコールバック関数を呼び出すことによって、デバイスが使用可能なでなくなったことをドライバーに通知します。 これらのコールバック関数の詳細については、次を参照してください。 [UMDF での PnP および電源管理のシナリオ](pnp-and-power-management-scenarios-in-umdf.md)します。

ドライバーを呼び出すことができます[ **IWDFIoTargetStateManagement::GetState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)ローカル I/O ターゲットの現在の状態を取得します。

### <a name="remote-io-target-states"></a>リモートの I/O ターゲットの状態

ドライバーを呼び出す必要があります[ **IWDFRemoteTarget::OpenFileByName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)または[ **IWDFRemoteTarget::OpenRemoteInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface)をリモートの I/O を開く対象とします。 ドライバーでは、リモートの I/O ターゲットが開いたら、フレームワークは、I/O ターゲットを自動的に開始します。

かどうか、必要に応じて、ドライバーを呼び出して[ **IWDFRemoteTarget::Stop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-stop) 、リモートの I/O のターゲットと呼び出しを一時的に停止する[ **IWDFRemoteTarget::Start** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-start)を再起動します。

リモートの I/O ターゲット デバイスが削除された場合、framework 自動的に停止して I/O ターゲットを閉じますおよびドライバーは、次のイベントのコールバック関数を登録しない限り、対象のキュー内にあるすべての I/O 要求を取り消します。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetqueryremove--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetQueryRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetqueryremove)  
リモートの I/O ターゲット デバイスを削除する可能性があります、ドライバーに通知します。 ドライバーを呼び出す必要があります[ **IWDFRemoteTarget::CloseForQueryRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-closeforqueryremove)ドライバー、デバイスの削除を許可するようにする場合。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetremovecomplete--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetRemoveComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetremovecomplete)  
リモートの I/O ターゲット デバイスが削除されたことをドライバーに通知します。 このコールバック関数を呼び出す必要があります[ **IWDFRemoteTarget::Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-close)します。

<a href="" id="---------iremotetargetcallbackremoval--onremotetargetremovecanceled--------"></a>[**IRemoteTargetCallbackRemoval::OnRemoteTargetRemoveCanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremotetargetcallbackremoval-onremotetargetremovecanceled)  
リモートの I/O ターゲット デバイスを削除する試行が取り消されたことをドライバーに通知します。 ドライバーを呼び出す必要があります、ドライバーを引き続き、ターゲットを使用する場合は、 [ **IWDFRemoteTarget::Reopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-reopen)します。 通常、ドライバーを呼び出します**再度開く**内から、 **OnRemoteTargetRemoveCanceled**コールバック関数が**再度開く**代わりに後に呼び出すことができます**OnRemoteTargetRemoveCanceled**を返します。

ドライバーを呼び出すことができます[ **IWDFRemoteTarget::GetState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-getstate)をリモートの I/O ターゲットの現在の状態を取得します。

 

 






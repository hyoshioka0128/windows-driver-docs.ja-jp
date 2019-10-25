---
title: 一般 I/O ターゲットの状態の制御
description: 一般 I/O ターゲットの状態の制御
ms.assetid: 37f756bf-b655-428e-b72c-f86c71f1a2db
keywords:
- '一般的な i/o ターゲット: WDK KMDF、状態'
- i/o ターゲット状態 WDK KMDF を開始しました
- 停止した i/o ターゲット状態 WDK KMDF
- クエリの終了-状態 WDK KMDF の削除
- 閉じた i/o ターゲット状態 WDK KMDF
- 削除された i/o ターゲット状態 WDK KMDF
- ローカル i/o ターゲット (WDK KMDF を)
- リモート i/o ターゲット (WDK KMDF を)
- i/o ターゲットを停止する WDK KMDF
- i/o ターゲットの再起動 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a543f43869ba34e932a53cc833395d8643ab8711
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843642"
---
# <a name="controlling-a-general-io-targets-state"></a>一般 I/O ターゲットの状態の制御


I/o ターゲットオブジェクトは、ゲートゲートとアウトゲートという2つのゲートを持つものとして視覚化できます。 Out ゲートは、フレームワークがターゲットデバイスオブジェクトに要求を配信するタイミングを制御します。一方、要求が i/o ターゲットに入ることを許可されている場合は、ゲートを制御します。

フレームワークは、一般的な i/o ターゲットに対して次の状態を定義します。

<a href="" id="started"></a>*開始*  
I/o ターゲットオブジェクトの両方のゲートが開いています。 ドライバーは i/o 要求を i/o ターゲットキューに送信でき、フレームワークは適切なドライバーに要求を配信します。

<a href="" id="stopped"></a>*なく*  
I/o ターゲットのゲートが開いていますが、out ゲートが閉じられています。 フレームワークは、適切なドライバーへの要求の配信を停止します。 I/o 要求を i/o ターゲットに送信するには、ドライバーは、 **WDF\_request\_send\_\_オプション**を設定する必要があります。これは\_\_ターゲット\_状態を無視するか、\_送信\_オプションを指定 @no__ **t_11_ SEND\_し、** 各要求の[**WDF\_要求\_\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options)の構造を送信する\_忘れます。

<a href="" id="purged"></a>*さ*  
I/o ターゲットオブジェクトの両方のゲートが閉じられています。 ドライバーは、 **WDF\_request\_send\_\_オプション**を設定しない限り、i/o 要求を i/o ターゲットに送信することはできません。ただし、\_ターゲット\_状態を無視するか、\_送信\_オプションを指定する必要があり **\_t_11_ を送信\_、忘れ\_** ます。 また、このフレームワークは、i/o ターゲットオブジェクトの内部キューにある未処理の要求をキャンセルします。 この状態は、KMDF バージョン1.11 以降で使用できます。

<a href="" id="closed-for-query-remove"></a>*クエリの終了-削除*  
リモート i/o ターゲットは、デバイスがすぐに削除される可能性があるため、一時的に閉じられています。

<a href="" id="closed"></a>*開閉*  
I/o ターゲットは閉じているため、開始または停止できません。

<a href="" id="deleted"></a>*削除*  
I/o ターゲットのデバイスは削除されています。

[**WDF\_IO\_ターゲット\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)列挙体は、これらの状態を表す値を定義します。 ドライバーは[**WdfIoTargetGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetgetstate)を呼び出して、i/o ターゲットの状態を取得できます。

### <a name="local-io-target-states"></a>ローカル i/o ターゲットの状態

フレームワークによって、ローカルの i/o ターゲットが自動的に開き、開始されます。

必要に応じて、ドライバーは[**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出してローカル i/o ターゲットを一時的に停止し、 [**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)を呼び出して再起動することができます。 たとえば、ドライバーは、一時的なエラー状態を検出し、エラー状態が修正された場合に i/o ターゲットを再起動すると、ローカル i/o ターゲットを停止することがあります。

KMDF バージョン1.11 以降では、ドライバーは[**Wdfiotargetpurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge)を呼び出して、i/o 要求がローカル i/o ターゲットに送信されるのを一時的に防止し、ターゲットのキュー内の未処理の要求をキャンセルすることができます。 たとえば、ファイルハンドルのクリーンアップの一部として、ドライバーに送信されたすべての要求が取り消されるように、ドライバーがローカル i/o ターゲットを削除する場合があります。

ローカル i/o ターゲットのデバイスが削除されると、フレームワークは自動的に i/o ターゲットを停止して閉じ、ターゲットのキューにあるすべての i/o 要求を[キャンセル](canceling-i-o-requests.md)します。 フレームワークは、デバイスオブジェクトイベントコールバック関数を呼び出すことによって、デバイスが使用できなくなったことをドライバーに通知します。 これらのコールバック関数の詳細については、「 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)」を参照してください。

### <a name="remote-io-target-states"></a>リモート i/o ターゲットの状態

ドライバーは、 [**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)を呼び出して、リモート i/o ターゲットを開く必要があります。 ドライバーがリモート i/o ターゲットを開くと、フレームワークは i/o ターゲットを自動的に開始します。

必要に応じて、ドライバーは[**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出して、リモート i/o ターゲットを一時的に停止し、 [**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)を呼び出して再起動することができます。

KMDF バージョン1.11 以降では、ドライバーは[**Wdfiotargetpurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge)を呼び出して、i/o 要求がリモート i/o ターゲットに送信されるのを一時的に防止し、ターゲットのキュー内の未処理の要求をキャンセルすることができます。

リモート i/o ターゲットのデバイスが削除されると、フレームワークは自動的に i/o ターゲットを停止して閉じ、次のイベントコールバック関数をドライバーが登録しない限り、ターゲットのキューにあるすべての i/o 要求をキャンセルします。

<a href="" id="evtiotargetqueryremove"></a>[*EvtIoTargetQueryRemove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)  
リモート i/o ターゲットのデバイスが削除される可能性があることをドライバーに通知します。 ドライバーでデバイスを削除できるようにするには、ドライバーが[**Wdfiotargetcloseforqueryremove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetcloseforqueryremove)を呼び出す必要があります。

<a href="" id="evtiotargetremovecomplete"></a>[*EvtIoTargetRemoveComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)  
リモート i/o ターゲットのデバイスが削除されたことをドライバーに通知します。 このコールバック関数は、 [**Wdfiotargetclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetclose)を呼び出す必要があります。

<a href="" id="evtiotargetremovecanceled"></a>[*EvtIoTargetRemoveCanceled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)  
リモート i/o ターゲットのデバイスを削除しようとしたことがキャンセルされたことをドライバーに通知します。 このコールバック関数は、 [**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)を呼び出す必要があります。通常、ドライバーは[**WDF\_io\_ターゲット\_呼び出し\_PARAMS を開い**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_reopen)て WDF\_IO\_ターゲットを初期化し\_\_PARAMS\_INIT 関数を開く (_s)

ドライバーがリモート i/o ターゲットの使用を終了し、ターゲットを再度使用しない場合に、ターゲットにまだ保留中の子要求オブジェクトがない場合、ドライバーは、最初に[**Wdfiotargetclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetclose)を呼び出さずに[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出すことができます。 ターゲットにまだ保留中の子要求オブジェクトがある場合、ドライバーは**Wdfobjectdelete**を安全に呼び出す前に、 **Wdfiotargetclose**を呼び出す必要があります。

 

 






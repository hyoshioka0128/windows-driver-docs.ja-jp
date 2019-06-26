---
title: 一般 I/O ターゲットの状態の制御
description: 一般 I/O ターゲットの状態の制御
ms.assetid: 37f756bf-b655-428e-b72c-f86c71f1a2db
keywords:
- 一般的な I/O WDK KMDF、状態をターゲットします。
- 対象の状態の I/O WDK KMDF の開始
- 対象の状態の I/O WDK KMDF の停止
- クエリの削除状態 WDK KMDF の終了
- 終了した I/O ターゲット状態 WDK KMDF
- 削除された I/O ターゲット状態 WDK KMDF
- ローカルの I/O WDK KMDF をターゲットします。
- リモートの I/O WDK KMDF をターゲットします。
- WDK KMDF を対象と I/O を停止しています
- WDK KMDF を対象と I/O を再起動します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af29ae3c9eb6400341b03e91218e02eb157b8ac8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382874"
---
# <a name="controlling-a-general-io-targets-state"></a>一般 I/O ターゲットの状態の制御


2 つのゲートを持つものとして I/O ターゲット オブジェクトを視覚化することができます。 ゲートでと、out-gate します。 フレームワークで、要求が、対象のデバイス オブジェクトを提供でゲート制御を要求のすべての I/O ターゲットを入力できる場合は、out-gate コントロール。

フレームワークには、次の状態の一般的な I/O ターゲットを定義します。

<a href="" id="started"></a>*開始*  
I/O のターゲット オブジェクトの両方のゲートは、開いています。 ドライバーは、I/O ターゲット キューに I/O 要求を送信することができ、フレームワークは、適切なドライバーを要求を配信します。

<a href="" id="stopped"></a>*停止*  
-ゲートの I/O ターゲットは起動していますが、out-gate が閉じられました。 フレームワークは、適切なドライバーへの要求の配信を停止します。 I/O ターゲットへの I/O 要求を送信するドライバー設定する必要がありますか**WDF\_要求\_送信\_オプション\_無視\_ターゲット\_状態**または**WDF\_要求\_送信\_オプション\_送信\_AND\_破棄**要求ごとに[ **WDF\_要求\_送信\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_send_options)構造体。

<a href="" id="purged"></a>*消去*  
I/O のターゲット オブジェクトの両方のゲートは閉じられます。 ドライバーは、設定しない限りに、I/O ターゲットへの I/O 要求を送信できません**WDF\_要求\_送信\_オプション\_無視\_ターゲット\_状態**または**WDF\_要求\_送信\_オプション\_送信\_AND\_破棄**します。 さらに、フレームワークは、I/O ターゲット オブジェクトの内部キュー内の未処理の要求をキャンセルします。 この状態で KMDF バージョン 1.11 以降を使用できます。

<a href="" id="closed-for-query-remove"></a>*クエリの削除の終了*  
リモートの I/O ターゲットはそのデバイスを削除できるだけ可能性がありますので、一時的に閉じられます。

<a href="" id="closed"></a>*終了*  
I/O ターゲットが閉じられると、開始または停止することはできません。

<a href="" id="deleted"></a>*削除*  
I/O ターゲットのデバイスが削除されました。

[ **WDF\_IO\_ターゲット\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)列挙は、これらの状態を表す値を定義します。 ドライバーを呼び出すことができます[ **WdfIoTargetGetState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetgetstate) I/O ターゲットの状態を取得します。

### <a name="local-io-target-states"></a>ローカル I/O ターゲットの状態

フレームワークは自動的に開き、ローカルの I/O ターゲットを起動します。

かどうか、必要に応じて、ドライバーを呼び出して[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)ローカルのターゲットの I/O および呼び出しを一時的に停止する[ **WdfIoTargetStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)に再起動します。 たとえば、ドライバーは、一時的なエラー条件を検出した場合は、ローカル I/O ターゲットを停止し、エラー状態が修正された場合に I/O ターゲットを再起動することが。

KMDF バージョン 1.11 以降でドライバーを呼び出すことが[ **WdfIoTargetPurge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge)一時的に I/O 要求がローカルな I/O ターゲットに送信されないようにすると、ターゲットのキュー内の未処理の要求をキャンセルします。 たとえば、ファイル ハンドルのクリーンアップの一環として、ドライバーがドライバーに送信されたすべての要求が取り消されることを確認するローカル I/O ターゲットを消去可能性があります。

フレームワークが自動的に停止し、I/O ターゲットを閉じる場合は、ローカルの I/O 対象のデバイスを削除すると、および[キャンセル](canceling-i-o-requests.md)ターゲットのキューにあるすべての I/O 要求。 フレームワークは、デバイス オブジェクトのイベントのコールバック関数を呼び出すことによって、デバイスが使用可能なでなくなったことをドライバーに通知します。 これらのコールバック関数の詳細については、次を参照してください。 [PnP および電源管理のシナリオ](pnp-and-power-management-scenarios.md)します。

### <a name="remote-io-target-states"></a>リモートの I/O ターゲットの状態

ドライバーを呼び出す必要があります[ **WdfIoTargetOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)をリモートの I/O ターゲットを開きます。 ドライバーでは、リモートの I/O ターゲットが開いたら、フレームワークは、I/O ターゲットを自動的に開始します。

かどうか、必要に応じて、ドライバーを呼び出して[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) 、リモートの I/O のターゲットと呼び出しを一時的に停止する[ **WdfIoTargetStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)に再起動します。

KMDF バージョン 1.11 以降でドライバーを呼び出すことが[ **WdfIoTargetPurge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge)一時的に I/O 要求がリモートの I/O ターゲットに送信されないようにすると、ターゲットのキュー内の未処理の要求をキャンセルするには.

リモートの I/O ターゲット デバイスが削除された場合、framework 自動的に停止して I/O ターゲットを閉じますおよびドライバーは、次のイベントのコールバック関数を登録しない限り、対象のキュー内にあるすべての I/O 要求を取り消します。

<a href="" id="evtiotargetqueryremove"></a>[*EvtIoTargetQueryRemove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)  
リモートの I/O ターゲット デバイスを削除する可能性があります、ドライバーに通知します。 ドライバーを呼び出す必要があります[ **WdfIoTargetCloseForQueryRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetcloseforqueryremove)ドライバー、デバイスの削除を許可するようにする場合。

<a href="" id="evtiotargetremovecomplete"></a>[*EvtIoTargetRemoveComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)  
リモートの I/O ターゲット デバイスが削除されたことをドライバーに通知します。 このコールバック関数を呼び出す必要があります[ **WdfIoTargetClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetclose)します。

<a href="" id="evtiotargetremovecanceled"></a>[*EvtIoTargetRemoveCanceled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)  
リモートの I/O ターゲット デバイスを削除する試行が取り消されたことをドライバーに通知します。 このコールバック関数を呼び出す必要があります[ **WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)、ドライバーの通常の呼び出しと[ **WDF\_IO\_ターゲット\_開く\_PARAMS\_INIT\_再度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_reopen) 、WDF を初期化するために\_IO\_ターゲット\_オープン\_PARAMS\_INIT 関数です。

ドライバーは、リモートの I/O ターゲットを使用して完了し、ターゲットをもう一度、使用しないターゲットには、まだ子要求オブジェクトがない場合、ドライバーを呼び出すことができます、保留中[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)せず呼び出す[ **WdfIoTargetClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetclose)します。 ターゲットが子要求オブジェクトは、まだ保留中のドライバーを呼び出す必要があります**WdfIoTargetClose**を安全に呼び出す前に**WdfObjectDelete**します。

 

 






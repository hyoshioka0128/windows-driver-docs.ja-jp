---
title: ユーザー モードとカーネル モード間のコミュニケーション
description: ユーザー モードとカーネル モード間のコミュニケーション
ms.assetid: ddfec0d0-ec7d-4f76-91b8-2cc34cfacf4e
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、通信サーバー ポート
- 通信サーバー ポート WDK ファイル システム ミニフィルター
- フィルター マネージャー WDK ファイル システム ミニフィルター、ユーザー モードまたはカーネル モードの通信
- カーネル モードの通信の WDK ファイル システム ミニフィルター
- ユーザー モードの通信の WDK ファイル システム ミニフィルター
- WDK、ファイル システム ミニフィルターのポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 119bc581262896fc42547fd484343e6c4da1506a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378984"
---
# <a name="communication-between-user-mode-and-kernel-mode"></a>ユーザー モードとカーネル モード間のコミュニケーション


フィルター マネージャーは、ユーザー モードとの通信のポート経由のカーネル モード間の通信をサポートします。 ミニフィルター ドライバーでは、通信ポートのオブジェクトに適用されるセキュリティ記述子を指定することで、ポートのセキュリティを制御します。 通信ポートを介した通信はバッファーされていないので、高速かつ効率的です。 ユーザー モード アプリケーションまたはサービスはメッセージに返信ミニフィルター ドライバーから双方向通信用。

ミニフィルター ドライバーは、通信サーバーのポートを作成し、着信接続をポートでリッスンするように暗黙的に開始します。 ユーザー モードの呼び出し元が、ポートに接続しようとすると、フィルター マネージャー呼び出しミニフィルター ドライバーの[ **ConnectNotifyCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatecommunicationport)ルーチンでは、新しく作成された接続を識別するハンドル。 フィルター マネージャーは、コントロールを再度獲得は、接続のユーザー モードの呼び出し元のエンドポイントを表す別のファイル ハンドルをユーザー モードの呼び出し元に渡します。 I/O 完了ポート リスナー ポートに関連付けるには、このハンドルを使用できます。

ユーザー モードの呼び出し元がポートのセキュリティ記述子で指定したとおりに十分なアクセス権を持つ場合にのみ、接続が受け入れられます。 ポートへの各接続は、独自のメッセージ キューとプライベート エンドポイントを取得します。

(カーネルまたはユーザー) のいずれかのエンドポイントを閉じるには、その接続が終了します。 ユーザー モードの呼び出し元は、エンドポイントへのハンドルを閉じ、フィルター マネージャー呼び出しミニフィルター ドライバーの[ **DisconnectNotifyCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatecommunicationport)ルーチン ミニフィルター ドライバーはハンドルを閉じることができますので、接続します。

通信サーバー ポートを閉じると、新しい接続できなくなりますが、既存の接続を終了しません。 フィルター マネージャーは、ミニフィルター ドライバーをアンロードするときに、既存の接続を終了します。

### <a name="span-idfiltermanagerroutinesforcommunicationbetweenusermodeandkernelmodespanspan-idfiltermanagerroutinesforcommunicationbetweenusermodeandkernelmodespanspan-idfiltermanagerroutinesforcommunicationbetweenusermodeandkernelmodespanfilter-manager-routines-for-communication-between-user-mode-and-kernel-mode"></a><span id="Filter_Manager_Routines_for_Communication_Between_User_Mode_and_Kernel_Mode"></span><span id="filter_manager_routines_for_communication_between_user_mode_and_kernel_mode"></span><span id="FILTER_MANAGER_ROUTINES_FOR_COMMUNICATION_BETWEEN_USER_MODE_AND_KERNEL_MODE"></span>ユーザー モードとカーネル モードの間の通信用フィルター マネージャー ルーチン

フィルター マネージャーは、ユーザー モード アプリケーションとの通信にミニフィルター ドライバー、カーネル モードの次のサポート ルーチンを提供します。

[**FltCloseClientPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcloseclientport)

[**FltCloseCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltclosecommunicationport)

[**FltCreateCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatecommunicationport)

[**FltSendMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsendmessage)

ミニフィルター ドライバーと通信するアプリケーションをユーザー モードでは、次のサポート ルーチンが提供されます。

[**FilterConnectCommunicationPort**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterconnectcommunicationport)

[**FilterGetMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetmessage)

[**FilterReplyMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterreplymessage)

[**FilterSendMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtersendmessage)

### <a name="span-idminifilterdrivercallbackroutinesforcommunicationbetweenusermodeandkernelmodespanspan-idminifilterdrivercallbackroutinesforcommunicationbetweenusermodeandkernelmodespanspan-idminifilterdrivercallbackroutinesforcommunicationbetweenusermodeandkernelmodespanminifilter-driver-callback-routines-for-communication-between-user-mode-and-kernel-mode"></a><span id="Minifilter_Driver_Callback_Routines_for_Communication_Between_User_Mode_and_Kernel_Mode"></span><span id="minifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_mode"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_COMMUNICATION_BETWEEN_USER_MODE_AND_KERNEL_MODE"></span>ユーザー モードとカーネル モードの間の通信に対してミニフィルター ドライバー コールバック ルーチン

次のミニフィルター ドライバー コールバック ルーチンをパラメーターとして渡される[ **FltCreateCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatecommunicationport):

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバック ルーチンの名前</th>
<th align="left">コールバック ルーチンの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ConnectNotifyCallback</em></p></td>
<td align="left"><p>PFLT_CONNECT_NOTIFY</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DisconnectNotifyCallback</em></p></td>
<td align="left"><p>PFLT_DISCONNECT_NOTIFY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>MessageNotifyCallback</em></p></td>
<td align="left"><p>PFLT_MESSAGE_NOTIFY</p></td>
</tr>
</tbody>
</table>

 

 

 





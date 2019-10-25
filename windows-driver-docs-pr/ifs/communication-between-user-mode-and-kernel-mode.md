---
title: ユーザー モードとカーネル モード間のコミュニケーション
description: ユーザー モードとカーネル モード間のコミュニケーション
ms.assetid: ddfec0d0-ec7d-4f76-91b8-2cc34cfacf4e
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、通信サーバーのポート
- 通信サーバーポート WDK ファイルシステムミニフィルター
- フィルターマネージャー WDK ファイルシステムミニフィルター、ユーザーモード/カーネルモード通信
- カーネルモード通信 WDK ファイルシステムミニフィルター
- ユーザーモード通信 WDK ファイルシステムミニフィルター
- ポート WDK、ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d47951164ac02ac83648c2f62f361a82095e7549
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841470"
---
# <a name="communication-between-user-mode-and-kernel-mode"></a>ユーザー モードとカーネル モード間のコミュニケーション


フィルターマネージャーは、通信ポートを使用したユーザーモードとカーネルモード間の通信をサポートしています。 ミニフィルタードライバーは、通信ポートオブジェクトに適用するセキュリティ記述子を指定することによって、ポートのセキュリティを制御します。 通信ポートを介した通信はバッファリングされないため、高速で効率的です。 ユーザーモードのアプリケーションまたはサービスは、ミニ転送ドライバーからのメッセージに応答して双方向通信を行うことができます。

ミニフィルタードライバーは、通信サーバーのポートを作成するときに、そのポートでの着信接続のリッスンを暗黙的に開始します。 ユーザーモードの呼び出し元がポートに接続しようとすると、フィルターマネージャーは、新しく作成された接続を処理するハンドルを使用して、ミニフィルタードライバーの[**Connectnotifycallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatecommunicationport)ルーチンを呼び出します。 フィルターマネージャーは制御を取り戻すと、ユーザーモードの呼び出し元を、接続に対するユーザーモードの呼び出し元のエンドポイントを表す別のファイルハンドルに渡します。 このハンドルを使用すると、i/o 完了ポートをリスナーポートに関連付けることができます。

接続は、ユーザーモードの呼び出し元が、ポートのセキュリティ記述子で指定されている十分なアクセス権を持っている場合にのみ受け入れられます。 ポートに接続するたびに、独自のメッセージキューとプライベートエンドポイントが取得されます。

いずれかのエンドポイント (カーネルまたはユーザー) を閉じると、その接続が終了します。 ユーザーモードの呼び出し元がエンドポイントへのハンドルを閉じると、フィルタマネージャーはミニフィルタードライバーの接続[**解除ルーチンを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatecommunicationport)呼び出し、ミニフィルタードライバーが接続のハンドルを閉じることができるようにします。

通信サーバーのポートを閉じると、新しい接続が防止されますが、既存の接続は終了しません。 フィルタマネージャは、ミニフィルタドライバがアンロードされたときに既存の接続を終了します。

### <a name="span-idfilter_manager_routines_for_communication_between_user_mode_and_kernel_modespanspan-idfilter_manager_routines_for_communication_between_user_mode_and_kernel_modespanspan-idfilter_manager_routines_for_communication_between_user_mode_and_kernel_modespanfilter-manager-routines-for-communication-between-user-mode-and-kernel-mode"></a><span id="Filter_Manager_Routines_for_Communication_Between_User_Mode_and_Kernel_Mode"></span><span id="filter_manager_routines_for_communication_between_user_mode_and_kernel_mode"></span><span id="FILTER_MANAGER_ROUTINES_FOR_COMMUNICATION_BETWEEN_USER_MODE_AND_KERNEL_MODE"></span>ユーザーモードとカーネルモード間の通信用フィルターマネージャールーチン

フィルターマネージャーには、ユーザーモードアプリケーションと通信するためのカーネルモードミニフィルタードライバーの次のサポートルーチンが用意されています。

[**FltCloseClientPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcloseclientport)

[**FltCloseCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclosecommunicationport)

[**FltCreateCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatecommunicationport)

[**FltSendMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsendmessage)

ユーザーモードアプリケーションがミニフィルタードライバーと通信するには、次のサポートルーチンが用意されています。

[**FilterConnectCommunicationPort**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterconnectcommunicationport)

[**FilterGetMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetmessage)

[**FilterReplyMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterreplymessage)

[**FilterSendMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtersendmessage)

### <a name="span-idminifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_modespanspan-idminifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_modespanspan-idminifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_modespanminifilter-driver-callback-routines-for-communication-between-user-mode-and-kernel-mode"></a><span id="Minifilter_Driver_Callback_Routines_for_Communication_Between_User_Mode_and_Kernel_Mode"></span><span id="minifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_mode"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_COMMUNICATION_BETWEEN_USER_MODE_AND_KERNEL_MODE"></span>ユーザーモードとカーネルモード間の通信用のミニフィルタードライバーコールバックルーチン

次のミニフィルタードライバーコールバックルーチンは、パラメーターとして[**FltCreateCommunicationPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatecommunicationport)に渡されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバックルーチン名</th>
<th align="left">コールバックルーチンの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ConnectNotifyCallback</em></p></td>
<td align="left"><p>PFLT_CONNECT_NOTIFY</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>切断 Notifycallback</em></p></td>
<td align="left"><p>PFLT_DISCONNECT_NOTIFY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>MessageNotifyCallback</em></p></td>
<td align="left"><p>PFLT_MESSAGE_NOTIFY</p></td>
</tr>
</tbody>
</table>

 

 

 





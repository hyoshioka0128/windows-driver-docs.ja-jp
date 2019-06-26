---
title: Winsock カーネルへの TDI ドライバーの移植
description: TDI ドライバーは、Winsock カーネル (WSK) を移植するには、次の表に示すように、WSK 対応 TDI タスクに変換する必要があります。
ms.assetid: 23662BF1-92EC-4C07-9A8D-F8F1D7D51692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f08c14e568f1f2c2399de4ca3127e2d30233709
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384535"
---
# <a name="porting-tdi-drivers-to-winsock-kernel"></a>Winsock カーネルへの TDI ドライバーの移植


TDI ドライバーは、Winsock カーネル (WSK) を移植するには、次の表に示すように、WSK 対応 TDI タスクに変換する必要があります。

| 処理手順                            | TDI                                                                                       | Winsock カーネル (WSK)                                                                                                          |
|----------------------------------|-------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| 登録し、登録解除          | なし                                                                                       | [**WskRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskregister)と[ **WskDeregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskderegister)                                       |
| キャプチャし、リリース プロバイダー NPI | なし                                                                                       | [**WskCaptureProviderNPI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskcaptureprovidernpi)と[ **WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskreleaseprovidernpi)   |
| ファイル オブジェクトのアドレスを作成します。       | 作成*EaBuffer*、呼び出して[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)                      | 必要なくなりました。 参照してください[ **WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)します。                                                                 |
| ファイルの接続オブジェクトを作成します。    | 接続作成*EaBuffer*、呼び出して[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)           | 必要なくなりました。 参照してください[ **WskSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)と[ *WskAcceptEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept_event)します。                 |
| アドレスを関連付ける                | [**TDI\_関連付ける\_アドレス**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565080(v=vs.85))                                | [**WskBind**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_bind)                                                                                               |
| イベント ハンドラーを設定します。               | [**TDI\_設定\_イベント\_ハンドラー**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | [**WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)または静的のバリエーションを使用して[ **WskControlClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client) |
| イベント ハンドラーをクリアします。             | [**TDI\_設定\_イベント\_ハンドラー**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | [**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)                                                                             |
| 接続                          | [**TDI\_接続**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565083(v=vs.85))                                                     | [**WskConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_connect)                                                                                         |
| 切断                       | [**TDI\_切断**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565090(v=vs.85))                                               | [**WskDisconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_disconnect)                                                                                   |
| Send                             | [**TDI\_送信**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565549(v=vs.85))                                                           | [**WskSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send)                                                                                               |
| Receive                          | [**TDI\_受信**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565131(v=vs.85))                                                     | [**WskReceive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive)                                                                                         |
| アドレスの関連付けを解除します。             | [**TDI\_関連付け解除\_アドレス**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565089(v=vs.85))                          | なし                                                                                                                           |
| 受信ハンドラー                  | [**ClientEventReceive**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545260(v=vs.85)), [**TDI\_RECEIVE**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565131(v=vs.85)) | [*WskReceiveEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_event)                                                                                 |
| ハンドラーを接続します。                  | [**ClientEventConnect**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff544257(v=vs.85)), [**TDI\_CONNECT**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565083(v=vs.85)) | [**WskAccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept)                                                                                           |
| ソケットまたは接続を閉じる       | [**ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)または[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)    | [**WskCloseSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_close_socket)                                                                                 |

 

 

 






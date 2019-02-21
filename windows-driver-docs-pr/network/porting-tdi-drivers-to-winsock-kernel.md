---
title: Winsock カーネルに TDI ドライバーの移植
description: TDI ドライバーは、Winsock カーネル (WSK) を移植するには、次の表に示すように、WSK 対応 TDI タスクに変換する必要があります。
ms.assetid: 23662BF1-92EC-4C07-9A8D-F8F1D7D51692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fbb55b0b9296abbad579ec82dd10d7bb622d7e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535339"
---
# <a name="porting-tdi-drivers-to-winsock-kernel"></a>Winsock カーネルに TDI ドライバーの移植


TDI ドライバーは、Winsock カーネル (WSK) を移植するには、次の表に示すように、WSK 対応 TDI タスクに変換する必要があります。

| タスク                            | TDI                                                                                       | Winsock カーネル (WSK)                                                                                                          |
|----------------------------------|-------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| 登録し、登録解除          | なし                                                                                       | [**WskRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff571143)と[ **WskDeregister**](https://msdn.microsoft.com/library/windows/hardware/ff571128)                                       |
| キャプチャし、リリース プロバイダー NPI | なし                                                                                       | [**WskCaptureProviderNPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571122)と[ **WskReleaseProviderNPI**](https://msdn.microsoft.com/library/windows/hardware/ff571145)   |
| ファイル オブジェクトのアドレスを作成します。       | 作成*EaBuffer*、呼び出して[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)                      | 必要なくなりました。 参照してください[ **WskSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571149)します。                                                                 |
| ファイルの接続オブジェクトを作成します。    | 接続作成*EaBuffer*、呼び出して[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)           | 必要なくなりました。 参照してください[ **WskSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571149)と[ *WskAcceptEvent*](https://msdn.microsoft.com/library/windows/hardware/ff571120)します。                 |
| アドレスを関連付ける                | [**TDI\_関連付ける\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/ff565080)                                | [**WskBind**](https://msdn.microsoft.com/library/windows/hardware/ff571121)                                                                                               |
| イベント ハンドラーを設定します。               | [**TDI\_設定\_イベント\_ハンドラー**](https://msdn.microsoft.com/library/windows/hardware/ff565576)                               | [**WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)または静的のバリエーションを使用して[ **WskControlClient**](https://msdn.microsoft.com/library/windows/hardware/ff571126) |
| イベント ハンドラーをクリアします。             | [**TDI\_設定\_イベント\_ハンドラー**](https://msdn.microsoft.com/library/windows/hardware/ff565576)                               | [**WskControlSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571127)                                                                             |
| 接続                          | [**TDI\_接続**](https://msdn.microsoft.com/library/windows/hardware/ff565083)                                                     | [**WskConnect**](https://msdn.microsoft.com/library/windows/hardware/ff571125)                                                                                         |
| 切断                       | [**TDI\_切断**](https://msdn.microsoft.com/library/windows/hardware/ff565090)                                               | [**WskDisconnect**](https://msdn.microsoft.com/library/windows/hardware/ff571129)                                                                                   |
| Send                             | [**TDI\_送信**](https://msdn.microsoft.com/library/windows/hardware/ff565549)                                                           | [**WskSend**](https://msdn.microsoft.com/library/windows/hardware/ff571146)                                                                                               |
| 受信                          | [**TDI\_受信**](https://msdn.microsoft.com/library/windows/hardware/ff565131)                                                     | [**WskReceive**](https://msdn.microsoft.com/library/windows/hardware/ff571139)                                                                                         |
| アドレスの関連付けを解除します。             | [**TDI\_関連付け解除\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/ff565089)                          | なし                                                                                                                           |
| 受信ハンドラー                  | [**ClientEventReceive**](https://msdn.microsoft.com/library/windows/hardware/ff545260), [**TDI\_RECEIVE**](https://msdn.microsoft.com/library/windows/hardware/ff565131) | [*WskReceiveEvent*](https://msdn.microsoft.com/library/windows/hardware/ff571140)                                                                                 |
| ハンドラーを接続します。                  | [**ClientEventConnect**](https://msdn.microsoft.com/library/windows/hardware/ff544257), [**TDI\_CONNECT**](https://msdn.microsoft.com/library/windows/hardware/ff565083) | [**WskAccept**](https://msdn.microsoft.com/library/windows/hardware/ff571109)                                                                                           |
| ソケットまたは接続を閉じる       | [**ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)または[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)    | [**WskCloseSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571124)                                                                                 |

 

 

 






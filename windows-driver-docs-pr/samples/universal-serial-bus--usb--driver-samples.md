---
title: USB (ユニバーサル シリアル バス) ドライバーのサンプル
description: このディレクトリにドライバーのサンプルでは、デバイスのカスタムの USB ドライバーを記述するための開始点を提供します。
ms.assetid: 4A61F62B-9C23-4265-8AB4-D3AB45F512DF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bcd2e4c90c6a4afc75721004a8d8d7e09a1bdb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330112"
---
# <a name="universal-serial-bus-usb-driver-samples"></a>USB (ユニバーサル シリアル バス) ドライバーのサンプル


このディレクトリにドライバーのサンプルでは、デバイスのカスタムの USB ドライバーを記述するための開始点を提供します。

## <a name="universal-serial-bus-usb"></a>ユニバーサル シリアル バス (USB)


| サンプル名                                                            | ソリューション                                                              | 説明                                                                                                                                                                         |
|------------------------------------------------------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| KMDF バス ドライバー                                                        | [kmdf\_enumswitches](https://go.microsoft.com/fwlink/p/?LinkId=618000) | KMDF をバス ドライバーの OSR usb-fx2 デバイスで使用する方法を示します。                                                                                                          |
| OSR usb-fx2 のサンプル KMDF 関数ドライバー                            | [kmdf\_fx2](https://go.microsoft.com/fwlink/p/?LinkId=620313)          | 一括を実行し、USB デバイスへのデータ転送を中断する方法を示します。 サンプルは、OSR usb-fx2 Learning Kit に書き込まれます。                                              |
| USB 関数クライアント ドライバー                                             | [ufxclientsample](https://go.microsoft.com/fwlink/p/?LinkId=620315)    | スケルトンのサンプル ドライバーを USB 関数クラスの拡張機能ドライバー (UFX) を使用して、Windows USB 関数のコント ローラーのドライバーを作成する方法を示します。                                     |
| OSR usb-fx2 (UMDF 1) の KMDF 関数ドライバー上記サンプル UMDF フィルター | [umdf\_filter\_kmdf](https://go.microsoft.com/fwlink/p/?LinkId=620316) | 上位のフィルター ドライバー、kmdf 上として UMDF フィルター ドライバーの読み込み方法を示します\_fx2 サンプル ドライバー。 サンプルは、OSR usb-fx2 Learning Kit に書き込まれます。                  |
| OSR usb-fx2 (UMDF 1) の UMDF 関数ドライバー上記サンプル UMDF フィルター | [umdf\_filter\_umdf](https://go.microsoft.com/fwlink/p/?LinkId=618001) | 上位のフィルター ドライバー、umdf 上として UMDF フィルター ドライバーの読み込み方法を示します\_fx2 サンプル ドライバー。 サンプルは、OSR usb-fx2 Learning Kit に書き込まれます。                  |
| UMDF 1 関数ドライバー                                                 | [umdf\_fx2](https://go.microsoft.com/fwlink/p/?LinkId=618002)          | OSR usb-fx2 デバイスのユーザー モード ドライバー フレームワーク (UMDF 1) ドライバー。 テスト アプリケーションとサンプルのデバイスのメタデータが含まれていて、権限借用とアイドル状態の電源をサポートします。 |
| UMDF 2 関数のドライバー                                                 | [umdf2\_fx2](https://go.microsoft.com/fwlink/p/?LinkId=618003)         | OSR usb-fx2 デバイスのユーザー モード ドライバー フレームワーク (UMDF 2) ドライバー。 テスト アプリケーションとサンプルのデバイスのメタデータが含まれていて、権限借用とアイドル状態の電源をサポートします。 |
| Usbsamp 汎用 USB ドライバー                                             | [usbsamp](https://go.microsoft.com/fwlink/p/?LinkId=618938)            | フル_スピード、高速、およびと一括と汎用の USB デバイスのアイソクロナス エンドポイントから SuperSpeed 転送を実行する方法を示します。                                    |
| USBView                                                                | [usbview](https://go.microsoft.com/fwlink/p/?LinkId=618004)            | Windows のアプリケーションで、すべての USB コント ローラーと、システムに接続されている USB デバイスを参照することができます。                                                                       |

 

 

 





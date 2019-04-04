---
title: USB I/O ターゲット
description: このセクションでは、KMDF と 2 の UMDF ドライバーがユニバーサル シリアル バス (USB) デバイスとやり取りする方法について説明します。
ms.assetid: 195c0f4b-7f33-428a-8de7-32643ad854c6
keywords:
- USB I/O ターゲット WDK KMDF、
- USB I/O ターゲット WDK KMDF
- USB 要求 WDK KMDF をブロックします。
- 翻訳の WDK KMDF
- USB I/O WDK KMDF をターゲットと USB I/O ターゲットの詳細について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29069f3c74bf38b656045d9c00a621e92881fa4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580181"
---
# <a name="usb-io-targets"></a>USB I/O ターゲット


このセクションでは、バージョン 2 以降では、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) のドライバーがユニバーサル シリアル バス (USB) デバイスとやり取りする方法について説明します。




各 USB デバイス、USB デバイスのインターフェイスをサポートする各パイプは、別の I/O ターゲットにあります。 コントロールでは、USB デバイス ハンドルが、デバイスの I/O のターゲットに送信されることを転送します。 特定のパイプ処理する I/O の転送は、そのパイプの I/O のターゲットに送信されます。

USB デバイスの I/O ターゲット USB 要求のブロックを送信することによって通信フレームワーク ([**翻訳**](https://msdn.microsoft.com/library/windows/hardware/ff538923))。 フレームワークは、構築自体を送信して、ドライバーがないように、ドライバーからの翻訳を非表示にするオブジェクトのメソッドを提供します。 ドライバーが翻訳を構築することをお望み、KMDF ドライバーは追加作成し、翻訳を送信するオブジェクトのメソッドのセットを使用できます。

USB デバイスの必要なドライバーの種類を確認する方法については、[USB クライアント ドライバーを開発するためのドライバー モデルを選択する](https://msdn.microsoft.com/library/windows/hardware/ff540215)を参照してください。

このセクションの内容:

-   [USB デバイスを使用してください。](working-with-usb-devices.md)

-   [USB インターフェイスの操作](working-with-usb-interfaces.md)

-   [USB パイプの使用](working-with-usb-pipes.md)

 

 






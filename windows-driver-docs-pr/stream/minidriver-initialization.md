---
title: ミニドライバーの初期化
description: ミニドライバーの初期化
ms.assetid: 5aa4e2c6-5848-45fe-8a89-686aae7e85e6
keywords:
- ストリーミング ミニドライバー WDK Windows 2000 のカーネルの初期化
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネル、ミニドライバーの初期化
- ストリーミング ミニドライバー WDK Windows 2000 のカーネルの初期化
- WDK Windows 2000 カーネル ストリーミング、ミニドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d7502aa337e0615baf215edc54ec96173335bb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577700"
---
# <a name="minidriver-initialization"></a>ミニドライバーの初期化





ミニドライバーの呼び出すようにミニドライバーは、まずオペレーティング システムに初期化**DriverEntry**ルーチン。 参照してください[ **Stream クラス ミニドライバーの DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff558717)します。 呼び出してにクラス ドライバーを使用した、ミニドライバーを登録する必要があります[ **StreamClassRegisterMinidriver**](https://msdn.microsoft.com/library/windows/hardware/ff568263)します。

ミニドライバー パス、 [ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682)クラス ドライバーをデバイス全体にわたるコールバックを含む、暫定的な情報を提供する構造体[ *StrMiniReceiveDevicePacket*](https://msdn.microsoft.com/library/windows/hardware/ff568463)、 [ *StrMiniCancelPacket*](https://msdn.microsoft.com/library/windows/hardware/ff568448)、 [ *StrMiniRequestTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff568473)、および[ *StrMiniInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff568459)します。

クラスのドライバーを使用し、 [ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463)デバイスを初期化する必要がありますが、ミニドライバーを通知します。 SRB 送信\_初期化\_デバイスの要求を渡します、 [**ポート\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567785)必要な構造体ハードウェアの情報。 この要求を完了すると、ミニドライバーがのバイト単位のサイズを指定、 [ **HW\_ストリーム\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff559686)構造がそのストリームのすべてを説明するために使用します。

クラスのドライバーを使用して、ミニドライバーは、その要求を完了すると、 [ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463) 、SRB を送信する\_取得\_ストリーム\_情報要求。 ミニドライバーは、すべての各ストリームのコールバックを含め、そのストリームに関する情報を提供します。

使用して、クラス ドライバーでは、ストリーム データの処理が完了すると、 [ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463) 、SRB を送信する\_初期化\_要求を完了します。 この時点で、ミニドライバーは、各ストリームで要求の処理を開始する準備が。

 

 





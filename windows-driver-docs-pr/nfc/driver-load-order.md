---
title: NFC ドライバーの読み込み順序
description: ACPI を表す NFCC、PnP デバイス ノードを作成する場合、に対して NFC クライアント ドライバーの .inf と一致して、そのデバイス ノードのインストールされます。
ms.assetid: 8094B525-A4A1-42D2-8D1F-4B32D77418E3
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0f1963fd4e4c58906bbdccd6fa2fa10b898c4df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370542"
---
# <a name="nfc-driver-load-order"></a>NFC ドライバーの読み込み順序


ACPI を表す NFCC、PnP デバイス ノードを作成する場合、に対して NFC クライアント ドライバーの .inf と一致して、そのデバイス ノードのインストールされます。 NFC のクライアント ドライバーは、その AddDevice ルーチンの中に初期化クラスの拡張により、Microsoft 提供の NFC クラス拡張 (NfcCx.dll) を読み込み、それ自体をできるようにセットアップ NFC クラスの最上部の開梱を任意の I/O キューを実装する必要があります。拡張機能ドライバー。 次の図は、ドライバーの読み込みメカニズムを示します。

![ドライバーの読み込み順序](images/driverloadsequence1.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  


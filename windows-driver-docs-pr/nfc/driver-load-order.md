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
ms.openlocfilehash: d1b3305bec5c9b69d4e846306244be1cc42261eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375235"
---
# <a name="nfc-driver-load-order"></a>NFC ドライバーの読み込み順序


ACPI を表す NFCC、PnP デバイス ノードを作成する場合、に対して NFC クライアント ドライバーの .inf と一致して、そのデバイス ノードのインストールされます。 NFC のクライアント ドライバーは、その AddDevice ルーチンの中に初期化クラスの拡張により、Microsoft 提供の NFC クラス拡張 (NfcCx.dll) を読み込み、それ自体をできるようにセットアップ NFC クラスの最上部の開梱を任意の I/O キューを実装する必要があります。拡張機能ドライバー。 次の図は、ドライバーの読み込みメカニズムを示します。

![ドライバーの読み込み順序](images/driverloadsequence1.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  


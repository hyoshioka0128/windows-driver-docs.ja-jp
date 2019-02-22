---
title: NFC ドライバーの読み込み順序
description: ACPI を表す NFCC、PnP デバイス ノードを作成する場合、に対して NFC クライアント ドライバーの .inf と一致して、そのデバイス ノードのインストールされます。
ms.assetid: 8094B525-A4A1-42D2-8D1F-4B32D77418E3
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1b3305bec5c9b69d4e846306244be1cc42261eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557303"
---
# <a name="nfc-driver-load-order"></a>NFC ドライバーの読み込み順序


ACPI を表す NFCC、PnP デバイス ノードを作成する場合、に対して NFC クライアント ドライバーの .inf と一致して、そのデバイス ノードのインストールされます。 NFC のクライアント ドライバーは、その AddDevice ルーチンの中に初期化クラスの拡張により、Microsoft 提供の NFC クラス拡張 (NfcCx.dll) を読み込み、それ自体をできるようにセットアップ NFC クラスの最上部の開梱を任意の I/O キューを実装する必要があります。拡張機能ドライバー。 次の図は、ドライバーの読み込みメカニズムを示します。

![ドライバーの読み込み順序](images/driverloadsequence1.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  


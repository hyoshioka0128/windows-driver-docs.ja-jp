---
title: 構成可能の有無
description: このトピックである拡張機能は、その操作の多くのパラメーターを構成するクライアント ドライバーを有効化、NFC クライアント ドライバーを使用可能なポイントします。
ms.assetid: 29C6C96E-9F20-4750-ABDD-103871B405FA
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63bdc7235c1291bd1fe2259585712197717af45d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375216"
---
# <a name="configurability"></a>構成可能の有無


NFC CX は NFC クライアント ドライバーに利用可能な機能拡張ポイント、だけでなく、その操作の多くのパラメーターを構成するクライアント ドライバーもできます。 NFC クライアント ドライバーでは、次の構成をカスタマイズできます。

-   ドライバーのフラグ
-   RF 探索の構成
-   LLCP 構成

## <a name="driver-flags"></a>ドライバーのフラグ


により、NFC のクライアント ドライバーを提供する、NFC CX [**ドライバー フラグ**](https://msdn.microsoft.com/library/windows/hardware/dn905542)クラスの拡張機能の実行時の実装を構成します。 これらのフラグは、NFC/CX NCI 仕様のあいまいさのためのさまざまなファームウェアの実装のため若干異なる方法では、特定の標準的な NCI 操作を実装を使用できます。

## <a name="rf-discovery-configuration"></a>RF 探索の構成


NFC クライアント ドライバーによって RF 探索の構成を設定できる、 [ **NfcCxSetRfDiscoveryConfig** ](https://msdn.microsoft.com/library/windows/hardware/dn905616)メソッド。 RF 探索の構成を呼び出した後の初期化中に行う必要があります[ **NfcCxDeviceInitialize**](https://msdn.microsoft.com/library/windows/hardware/dn905611)、それ以外の場合、エラーが返されます。

## <a name="llcp-configuration"></a>LLCP 構成


NFC クライアント ドライバーによって LLCP 構成を設定することができます、 [ **NfcCxSetLlcpConfig** ](https://msdn.microsoft.com/library/windows/hardware/dn905615) NFC CX によって提供されるメソッド。 LLCP 構成は、後の初期化中に行う必要があります[ **NfcCxDeviceInitialize**](https://msdn.microsoft.com/library/windows/hardware/dn905611)、それ以外の場合、エラーが返されます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

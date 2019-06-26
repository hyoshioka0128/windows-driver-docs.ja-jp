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
ms.openlocfilehash: c91788077e4e1b6e7a0f4b4d0f60e8c811cc0dcf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377553"
---
# <a name="configurability"></a>構成可能の有無


NFC CX は NFC クライアント ドライバーに利用可能な機能拡張ポイント、だけでなく、その操作の多くのパラメーターを構成するクライアント ドライバーもできます。 NFC クライアント ドライバーでは、次の構成をカスタマイズできます。

-   ドライバーのフラグ
-   RF 探索の構成
-   LLCP 構成

## <a name="driver-flags"></a>ドライバーのフラグ


により、NFC のクライアント ドライバーを提供する、NFC CX [**ドライバー フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/ne-nfccx-_nfc_cx_driver_flags)クラスの拡張機能の実行時の実装を構成します。 これらのフラグは、NFC/CX NCI 仕様のあいまいさのためのさまざまなファームウェアの実装のため若干異なる方法では、特定の標準的な NCI 操作を実装を使用できます。

## <a name="rf-discovery-configuration"></a>RF 探索の構成


NFC クライアント ドライバーによって RF 探索の構成を設定できる、 [ **NfcCxSetRfDiscoveryConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)メソッド。 RF 探索の構成を呼び出した後の初期化中に行う必要があります[ **NfcCxDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxdeviceinitialize)、それ以外の場合、エラーが返されます。

## <a name="llcp-configuration"></a>LLCP 構成


NFC クライアント ドライバーによって LLCP 構成を設定することができます、 [ **NfcCxSetLlcpConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxsetllcpconfig) NFC CX によって提供されるメソッド。 LLCP 構成は、後の初期化中に行う必要があります[ **NfcCxDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxdeviceinitialize)、それ以外の場合、エラーが返されます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

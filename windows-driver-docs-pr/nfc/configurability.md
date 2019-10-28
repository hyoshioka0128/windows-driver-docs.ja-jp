---
title: 構成可能の有無
description: このトピックでは、NFC クライアントドライバーが使用できる機能拡張ポイントを discuses します。これにより、クライアントドライバーは多くの操作のパラメーターを構成できるようになります。
ms.assetid: 29C6C96E-9F20-4750-ABDD-103871B405FA
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5be86a42d07ddbca4e2a3a755ead62003d31f038
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843429"
---
# <a name="configurability"></a>構成可能の有無


Nfc クライアントドライバーで使用できる機能拡張ポイントに加えて、NFC CX では、クライアントドライバーが多くの操作のパラメーターを構成することもできます。 次の構成は、NFC クライアントドライバーでカスタマイズできます。

-   ドライバーフラグ
-   RF 検出の構成
-   LLCP 構成

## <a name="driver-flags"></a>ドライバーフラグ


NFC CX を使用すると、NFC クライアントドライバーは、クラス拡張の実行時実装を構成するための[**ドライバーフラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ne-nfccx-_nfc_cx_driver_flags)を提供できます。 これらのフラグにより、NFC CX は、NCI 仕様のあいまいさのために、ファームウェアの実装が異なるため、特定の標準 NCI 操作を若干異なる方法で実装できます。

## <a name="rf-discovery-configuration"></a>RF 検出の構成


RF 探索の構成は、 [**NfcCxSetRfDiscoveryConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)メソッドを使用して、NFC クライアントドライバーによって設定できます。 RF 検出構成は、 [**Nfccxdeviceinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)を呼び出した後に初期化中に実行する必要があります。そうしないと、エラーが返されます。

## <a name="llcp-configuration"></a>LLCP 構成


LLCP 構成は、nfc CX によって提供される[**Nfccxsetllcpconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetllcpconfig)メソッドを使用して、nfc クライアントドライバーによって設定できます。 LLCP 構成は、 [**Nfccxdeviceinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)の後の初期化中に実行する必要があります。そうしないと、エラーが返されます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

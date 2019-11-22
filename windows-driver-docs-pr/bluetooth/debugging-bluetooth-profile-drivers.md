---
title: Bluetooth プロファイル ドライバーのデバッグ
description: Bluetooth プロファイル ドライバーのデバッグ
ms.assetid: 3c04017e-7f5c-49d4-ad7e-36c7405133a1
keywords:
- プロファイルドライバーのデバッグ WDK Bluetooth
- Bluetooth WDK、デバッグプロファイルドライバー
- ドライバーのデバッグ WDK Bluetooth
- プロファイルドライバー WDK Bluetooth、デバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274fd22c31a334ae9c4b19a335574231939146c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833853"
---
# <a name="debugging-bluetooth-profile-drivers"></a>Bluetooth プロファイル ドライバーのデバッグ


Bluetooth プロファイルドライバーを開発するときに、ドライバーの[検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)を使用して、デバッグを支援することができます。

検証チェックを有効にするには、 [Bthusb. sys のドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-drivers-to-be-verified)機能を有効にする必要があります。 この操作を行わない場合、検証チェックは無効になります。

検証チェックを完全に利用するには、bluetooth 要求ブロック (BRB) の割り当てルーチン (たとえば、 [**Bthallocatebrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_allocate_brb)や[**Bthinitializebrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_initialize_brb)など[) を使用](building-and-sending-a-brb.md)します。これは、bluetooth ドライバースタックによって提供されます。 これらのルーチンには、プロファイルドライバーのデバッグに役立つ追加機能が含まれています。

検証チェックは、次の種類のエラーをキャッチするのに役立ちます。

-   完了前に BRB を再送信しようとします

-   無効な BRB 型の割り当てまたは初期化を試行します

-   無効なサイズの BRB の送信を試みます

プロファイルドライバーをデバッグしているときに、エラーの説明を取得するために、BC\_BLUETOOTH\_検証ツール\_エラーの後に、 **! analyze-v**デバッガーコマンドを使用できます。

 

 






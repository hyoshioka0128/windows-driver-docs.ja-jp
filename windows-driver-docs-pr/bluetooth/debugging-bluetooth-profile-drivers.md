---
title: Bluetooth のプロファイルのドライバーのデバッグ
description: Bluetooth のプロファイルのドライバーのデバッグ
ms.assetid: 3c04017e-7f5c-49d4-ad7e-36c7405133a1
keywords:
- プロファイル ドライバー WDK Bluetooth のデバッグ
- Bluetooth の WDK、プロファイルのドライバーのデバッグ
- ドライバー WDK Bluetooth のデバッグ
- ドライバー WDK の Bluetooth のプロファイルのデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecaf8b97b1ce29faf84cecef41e4e5d7f339d44e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551139"
---
# <a name="debugging-bluetooth-profile-drivers"></a>Bluetooth のプロファイルのドライバーのデバッグ


使用することができます、Bluetooth プロファイル ドライバーを開発するときに[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)のデバッグが支援します。

必要な検証チェックを有効にする[Bthusb.sys の Driver Verifier を有効にする](https://msdn.microsoft.com/library/windows/hardware/ff551729)します。 これを行わない場合は、検証チェックが無効になります。

検証を利用するチェック完全には、確認、Bluetooth 要求ブロック (BRB) 割り当てルーチンを使用すると、たとえば、 [ **BthAllocateBrb** ](https://msdn.microsoft.com/library/windows/hardware/ff536634)と[ **BthInitializeBrb**](https://msdn.microsoft.com/library/windows/hardware/ff536639)、Bluetooth ドライバー スタックが用意されている[ビルドおよび送信 BRBs](building-and-sending-a-brb.md)します。 これらのルーチンには、プロファイルのドライバーのデバッグに役立つ追加の機能が含まれます。

検証チェックは、次のようなエラーをキャッチできます。

-   完了する前に、BRB を再送信しようとしています。

-   割り当てるか、無効な BRB を初期化する試行を入力します。

-   無効なサイズの BRB を送信しようとしています。

プロファイルには、ドライバー、デバッグ中に使用することができます、 **! 分析 v** BC 後のデバッガー コマンド\_BLUETOOTH\_VERIFIER\_障害エラーの説明を取得します。

 

 






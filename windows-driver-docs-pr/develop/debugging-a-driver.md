---
ms.assetid: 2274e848-2a0b-445c-82cd-7bcd9e23078a
title: ドライバーのデバッグ
description: 通常、カーネル モード ドライバーのデバッグには、2 台のコンピューターが必要です。
ms.date: 08/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 11ce11eb481fe21d476dfdac97b109c253c3eb4f
ms.sourcegitcommit: 2231d322eb4e9597ad7f537a4aa82b83422bd46a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70020685"
---
# <a name="debugging-a-driver"></a>ドライバーのデバッグ

カーネル モード ドライバーのデバッグには、2 台のコンピューターが必要です。 デバッガーは*ホスト コンピューター*上で実行され、デバッグ対象のコードは*ターゲット コンピューター*上で実行されます。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 ユーザー モード ドライバーは、ホスト コンピューター上でも、別のターゲット コンピューター上でもデバッグできます。 ターゲット コンピューター上で実行されているドライバーをデバッグする前に、ターゲット コンピューターをデバッグ用に構成する必要があります。

デバッガー ドライバーについて詳しくは、「[Windows のデバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windows-debugging)」をご覧ください。

ターゲット コンピューターの構成と、ネットワーク接続を使用したデバッグ ケーブルの設定については、「[KDNET ネットワーク カーネル デバッグの自動設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)」をご覧ください。

## <a name="see-also"></a>参照

[Windows のデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

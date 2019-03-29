---
title: AVStream コーデックのハードウェア メディアの使用
description: AVStream コーデックのハードウェア メディアの使用
ms.assetid: 07c25875-c549-4d47-ac0d-605f2aa9daa4
keywords:
- AVStream ハードウェア コーデックは、ハードウェアのメディアを使用して、WDK をサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e244540a8f89636a248eee17e6366966a6fe0dbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573867"
---
# <a name="using-hardware-mediums-in-avstream-codecs"></a>AVStream コーデックのハードウェア メディアの使用


プライベートのメディアをサポートする AVStream ミニドライバーは、デバイスのハードウェア、システム メモリへの中間の転送せずにデータを転送できます。

具体的には、2 つのフィルターは、同じプライベート中規模および中規模のインスタンスを共有している場合、メディア ファンデーションはデバイスのハードウェアに排他的にメディアを転送します。 この転送は、システム メモリをせず、関数は発生します。 たとえば、デコーダーおよびエンコーダーを同じデバイスからは、プライベート中規模でパフォーマンスを大幅に向上したを共有できます。

プライベートのメディアを使用する、ミニドライバーは、pin のでは、次を行う必要があります[ *AVStrMiniPinProcess* ](https://msdn.microsoft.com/library/windows/hardware/ff556351)関数。

1.  暗証番号 (pin) の接続中 が選択されている場合は、ドライバーのカスタム (たとえば、暗証番号 (pin) の中でない KSMEDIUMSETID\_標準)、ドライバーは、プライベートのバスを使用してデータをルーティングする必要があります。 AVStream はストリーム ポインター トランスポート カスタム メディアを使用して接続されている pin を有効になりません。

2.  ドライバーを呼び出すことによって接続されている pin 調べる[ **KsPinGetConnectedPinFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff563508)します。

3.  ドライバーは、バッファーでの操作を実行し、カスタム メディアを介して接続されている pin/フィルター オブジェクトにルーティングします。

 

 





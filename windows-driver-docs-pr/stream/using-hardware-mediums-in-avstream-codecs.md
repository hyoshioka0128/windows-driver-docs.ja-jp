---
title: AVStream コーデックのハードウェア メディアの使用
description: AVStream コーデックのハードウェア メディアの使用
ms.assetid: 07c25875-c549-4d47-ac0d-605f2aa9daa4
keywords:
- AVStream ハードウェア コーデックは、ハードウェアのメディアを使用して、WDK をサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 689cfa6d7a8d6d9b503142b440b1dba48da27cf3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381124"
---
# <a name="using-hardware-mediums-in-avstream-codecs"></a>AVStream コーデックのハードウェア メディアの使用


プライベートのメディアをサポートする AVStream ミニドライバーは、デバイスのハードウェア、システム メモリへの中間の転送せずにデータを転送できます。

具体的には、2 つのフィルターは、同じプライベート中規模および中規模のインスタンスを共有している場合、メディア ファンデーションはデバイスのハードウェアに排他的にメディアを転送します。 この転送は、システム メモリをせず、関数は発生します。 たとえば、デコーダーおよびエンコーダーを同じデバイスからは、プライベート中規模でパフォーマンスを大幅に向上したを共有できます。

プライベートのメディアを使用する、ミニドライバーは、pin のでは、次を行う必要があります[ *AVStrMiniPinProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin)関数。

1.  暗証番号 (pin) の接続中 が選択されている場合は、ドライバーのカスタム (たとえば、暗証番号 (pin) の中でない KSMEDIUMSETID\_標準)、ドライバーは、プライベートのバスを使用してデータをルーティングする必要があります。 AVStream はストリーム ポインター トランスポート カスタム メディアを使用して接続されている pin を有効になりません。

2.  ドライバーを呼び出すことによって接続されている pin 調べる[ **KsPinGetConnectedPinFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetconnectedpinfileobject)します。

3.  ドライバーは、バッファーでの操作を実行し、カスタム メディアを介して接続されている pin/フィルター オブジェクトにルーティングします。

 

 





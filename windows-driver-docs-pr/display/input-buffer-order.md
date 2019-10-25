---
title: 入力バッファー順序
description: 入力バッファー順序
ms.assetid: 99110b1a-1511-44f5-a4bb-a5e38fd41fff
keywords:
- 入力バッファー WDK DirectX VA
- WDK DirectX VA のノンインターレース、入力バッファーの順序
- バッファー WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e828c0ff5a9312ec4f5868f9275a342dd4ac3ef6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840360"
---
# <a name="input-buffer-order"></a>入力バッファー順序


## <span id="ddk_input_buffer_order_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_GG"></span>


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

VMR は、各組み合わせのノンインターレース化とサブストリーム合成操作に対して、ドライバーが提供する[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しを開始します。 *Ddmocomprender*呼び出しでは、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体の**lpbufferinfo**メンバーが、ターゲットサーフェスと各入力ビデオソースサンプルのサーフェイスを記述するバッファーの配列を指しています。 さらに、 *Ddmocomprender*関数は、ドライバーの[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数を呼び出します。 詳細については、「[ユーザーモードコンポーネントからのノンインターレース DDI の呼び出し](calling-the-deinterlace-ddi-from-a-user-mode-component.md)」を参照してください。

[**DXVA\_DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)構造体の**ソース**メンバー内にある[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体の配列内の要素の順序は、 **lpbufferinfo**配列と、変換先の例外と一致します。surface が存在しません。

次のトピックでは、 **Lpbufferinfo**配列にサーフェイスを配置するための規則について説明し、サーフェスのシーケンス順序を説明する例を示します。

[入力バッファーの順序の規則](input-buffer-order-rules.md)

[入力バッファーの順序の例1](input-buffer-order-example-1.md)

[入力バッファーの順序の例2](input-buffer-order-example-2.md)

[入力バッファーの順序の例3](input-buffer-order-example-3.md)

[入力バッファーの順序の例4](input-buffer-order-example-4.md)

[入力バッファーの順序の例5](input-buffer-order-example-5.md)

[入力バッファーの順序の例6](input-buffer-order-example-6.md)

 

 






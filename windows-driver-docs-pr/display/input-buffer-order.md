---
title: 入力バッファー順序
description: 入力バッファー順序
ms.assetid: 99110b1a-1511-44f5-a4bb-a5e38fd41fff
keywords:
- 入力バッファーの WDK DirectX VA
- デインター レースの WDK DirectX va なので、入力バッファーの順序
- WDK DirectX VA をバッファー処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f35699f8c5c4ceebcabf9273fb7c5329bc957a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379914"
---
# <a name="input-buffer-order"></a>入力バッファー順序


## <span id="ddk_input_buffer_order_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

VMR を各組み合わせデインター レース、サブストリームの複合操作の場合に、ドライバーによって提供されるへの呼び出しを開始します[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数。 *DdMoCompRender*を呼び出すには、 **lpBufferInfo**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)へのポインターを構造体、宛先表面、および各入力ビデオ ソース サンプルの画面について説明するバッファーの配列。 *DdMoCompRender*関数を呼び出してドライバーの[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数。 詳細については、次を参照してください。[ユーザー モード コンポーネントからインター レースを解除 DDI を呼び出す](calling-the-deinterlace-ddi-from-a-user-mode-component.md)します。

配列内の要素の順序[ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)内の構造体、**ソース**のメンバー、 [ **DXVA\_DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex)と一致する構造体、 **lpBufferInfo**宛先表面が存在しないこと、例外を持つ配列です。

次のトピックの表面に配置するときの規則の説明、 **lpBufferInfo**配列し、サーフェスの順序を説明する例を示します。

[入力バッファーの順序ルール](input-buffer-order-rules.md)

[入力バッファーの順序の例 1](input-buffer-order-example-1.md)

[入力バッファーの順序の例 2](input-buffer-order-example-2.md)

[入力バッファー順序例 3](input-buffer-order-example-3.md)

[入力バッファー順序例 4](input-buffer-order-example-4.md)

[入力バッファー順序例 5](input-buffer-order-example-5.md)

[入力バッファー順序例 6](input-buffer-order-example-6.md)

 

 






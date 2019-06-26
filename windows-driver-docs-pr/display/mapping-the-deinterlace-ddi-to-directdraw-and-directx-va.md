---
title: DirectDraw および DirectX VA へのデインターレース DDI のマッピング
description: DirectDraw および DirectX VA へのデインターレース DDI のマッピング
ms.assetid: a060265f-e1a2-416c-8533-6971cc9e2156
keywords:
- WDK DirectX va なので、マッピング デインター レース DDI デインター レース
- DDI デインター レース マッピング
- WDK DirectX VA にコンテナー メソッド
- デバイス メソッド WDK DirectX VA
- 動き補正 WDK DirectX VA
- WDK DirectX VA のコールバック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ca7b655e5bef9973b680676221bbefeedd700ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370124"
---
# <a name="mapping-the-deinterlace-ddi-to-directdraw-and-directx-va"></a>DirectDraw および DirectX VA へのデインターレース DDI のマッピング


## <span id="ddk_mapping_the_deinterlace_ddi_to_directdraw_and_directx_va_gg"></span><span id="DDK_MAPPING_THE_DEINTERLACE_DDI_TO_DIRECTDRAW_AND_DIRECTX_VA_GG"></span>


DirectDraw のを介してアクセスする必要があります機能デインター レース[補正コールバック関数のモーション](motion-compensation-callbacks.md)を[DDI インター レースを解除](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-ddi)マップすることができます。

DDI は 2 つの機能グループに分かれていますインター: DirectX VA コンテナーのメソッドおよび DirectX VA デバイスのメソッド。 コンテナーのメソッドは、ディスプレイ ハードウェアに格納されている各 DirectX VA デバイスの機能を決定します。 デバイスのメソッドは、デバイスに固有の操作を実行するデバイスを指示します。 DirectX VA ドライバーでは、1 つだけのコンテナーを使用できますが、複数のデバイスをサポートできます。

型指定されたパラメーターを使用しないためインター DDI を動き補正のコールバックにマップすることは (これは、1 つのパラメーターが、構造体へのポインターがある)。 つまり、その情報の種類に従って動き補正のコールバック関数に渡される 1 つのパラメーターの情報を処理できます。 たとえば場合、 **DXVA\_DeinterlaceBltFnCode**-に型情報が渡される、 [ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)関数、 *DdMoCompRender*呼び出すことができます、 [ **DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)のインター DDI ビデオ ストリーム オブジェクトのビット ブロック インターを実行する関数。 ただし場合、 **DXVA\_DeinterlaceQueryModeCapsFnCode**-に型情報が渡される*DdMoCompRender*代わりに、 *DdMoCompRender* を呼び出すことができます[**DeinterlaceQueryModeCaps** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)デインター レース モードの機能を照会するインター DDI の関数。

次のトピックでは、モーションの補正コールバックにインター DDI をマップする方法について説明します。

[コンテナー デバイス デインター レースをインター レースを解除します。](deinterlace-container-device-for-deinterlacing.md)

[呼び出し、ユーザー モード コンポーネントから DDI インター レースを解除](calling-the-deinterlace-ddi-from-a-user-mode-component.md)

 

 






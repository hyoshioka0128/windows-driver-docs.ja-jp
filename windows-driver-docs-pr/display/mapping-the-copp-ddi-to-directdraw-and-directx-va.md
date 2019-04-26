---
title: DirectDraw および DirectX VA への COPP DDI のマッピング
description: DirectDraw および DirectX VA への COPP DDI のマッピング
ms.assetid: 737dabab-39f0-44fd-9d34-56d812ffde88
keywords:
- コピー防止 WDK COPP、COPP DDI のマッピング
- ビデオのコピー防止 WDK COPP、COPP DDI のマッピング
- COPP WDK DirectX va なので、COPP DDI のマッピング
- マッピング COPP DDI、保護対象のビデオの WDK COPP
- COPP DDI WDK DirectX VA のマッピング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5793feb0cc669e966f9cc29ffddfccaf17a427c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358422"
---
# <a name="mapping-the-copp-ddi-to-directdraw-and-directx-va"></a>DirectDraw および DirectX VA への COPP DDI のマッピング


## <span id="ddk_mapping_the_copp_ddi_to_directdraw_and_directx_va_gg"></span><span id="DDK_MAPPING_THE_COPP_DDI_TO_DIRECTDRAW_AND_DIRECTX_VA_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

COPP 機能からアクセスする必要があります、[補正コールバック関数のモーション](motion-compensation-callbacks.md)DirectDraw、先の[COPP DDI](sample-functions-for-copp.md)マップすることができます。 ディスプレイ ドライバーである必要があります COPP DDI はビデオのミニポート ドライバーに実装されているため、 [COPP Ioctl を使用して、ビデオのミニポート ドライバーと通信](communicating-ioctls-to-the-video-miniport-driver.md)します。

型指定されたパラメーターを使用しないため COPP DDI は動き補正のコールバック関数にマップできる (これは、1 つのパラメーターが、構造体へのポインターがある)。 つまり、その情報の種類に従って動き補正のコールバック関数に渡される 1 つのパラメーターの情報を処理できます。

たとえば場合、 **DXVA\_COPPGetCertificateLengthFnCode**-に型情報が渡される、 [ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)関数は、[ *DdMoCompRender*呼び出しを開始することができます、 [ *COPPGetCertificateLength* ](https://msdn.microsoft.com/library/windows/hardware/ff539644)のグラフィックスで使用される証明書の長さ (バイト単位) を照会する COPP DDI 関数ハードウェア。 ただし場合、 **DXVA\_COPPSequenceStartFnCode**-に型情報が渡される*DdMoCompRender*代わりに、 *DdMoCompRender*への呼び出しを開始できます[ *COPPSequenceStart* ](https://msdn.microsoft.com/library/windows/hardware/ff540421)の現在のビデオ セッションで保護されているコマンドと状態のシーケンスの開始を示す COPP DDI 関数。

次のトピックでは、COPP DDI を動き補正のコールバック関数にマップする方法について説明します。

[DirectX VA COPP デバイス](directx-va-copp-device.md)

[ユーザー モード コンポーネントから COPP DDI を呼び出す](calling-the-copp-ddi-from-a-user-mode-component.md)

[ディスプレイ ドライバーから COPP DDI の呼び出し](calling-the-copp-ddi-from-the-display-driver.md)

 

 






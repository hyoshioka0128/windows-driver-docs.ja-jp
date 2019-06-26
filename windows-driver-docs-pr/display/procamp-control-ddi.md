---
title: ProcAmp コントロール DDI
description: ProcAmp コントロール DDI
ms.assetid: 102e21eb-bad4-4ab5-8630-9ac37c33f20a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: b9486031e8cf599a69858d56c5337a3ee8c8fcaa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363720"
---
# <a name="procamp-control-ddi"></a>ProcAmp コントロール DDI


## <span id="ddk_procamp_control_ddi_gg"></span><span id="DDK_PROCAMP_CONTROL_DDI_GG"></span>


ビデオの混在レンダラー (VMR) が ProcAmp コントロールの機能にアクセスできるように、ディスプレイ ドライバーが実装する必要があります、[補正コールバック関数のモーション](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

ドライバーの開発を簡略化するのには、動き補正コード テンプレートを使用し、このセクションでは ProcAmp コントロール関数を実装します。 関数は、インター コンテナー デバイスまたはデバイスの ProcAmp コントロール クラスのメンバー関数です。 詳細については、次を参照してください。[インター レースを解除するコンテナー デバイス クラスを定義する](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-deinterlace-container-device-class)と[ProcAmp コントロール デバイス クラスを定義する](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-procamp-control-device-class)します。

 

 






---
title: ProcAmp コントロール DDI
description: ProcAmp コントロール DDI
ms.assetid: 102e21eb-bad4-4ab5-8630-9ac37c33f20a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae0e05b61ce8ad985e76bf881b27f7e5ce621bca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829692"
---
# <a name="procamp-control-ddi"></a>ProcAmp コントロール DDI


## <span id="ddk_procamp_control_ddi_gg"></span><span id="DDK_PROCAMP_CONTROL_DDI_GG"></span>


ビデオミキシングレンダラー (VMR) が ProcAmp の機能にアクセスできるようにするには、ディスプレイドライバーが[モーション補正コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を実装する必要があります。

ドライバーの開発を簡略化するには、モーション補正コードテンプレートを使用し、このセクションの ProcAmp コントロール関数を実装します。 関数は、ノンインターレースコンテナーデバイスクラスまたは ProcAmp control デバイスクラスのメンバー関数です。 詳細については、「[ノンインターレースコンテナーデバイスクラスの定義](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-deinterlace-container-device-class)」および「 [ProcAmp コントロールデバイスクラスの定義](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-procamp-control-device-class)」を参照してください。

 

 






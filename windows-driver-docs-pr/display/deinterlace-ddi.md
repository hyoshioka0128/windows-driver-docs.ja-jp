---
title: デインターレース DDI
description: デインターレース DDI
ms.assetid: 06b85f76-950a-4a9b-af6b-ded823bfda6a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7b59f2cb6ee4da8048a37bdb144413d028987519
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839762"
---
# <a name="deinterlace-ddi"></a>デインターレース DDI


## <span id="ddk_deinterlace_ddi_gg"></span><span id="DDK_DEINTERLACE_DDI_GG"></span>


ビデオミキシングレンダラー (VMR) でビデオコンテンツのインターレースを解除し、フレームレート変換を実行できるようにするには、ディスプレイドライバーが[モーション補正コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を実装する必要があります。

ドライバーの開発を簡略化するには、モーション補正コードテンプレートを使用し、このセクションのノンインターレース関数を実装します。 関数は、ノンインターレースコンテナーデバイスクラスまたはノンインターレースモードデバイスクラスのメンバー関数です。 詳細については、「[ノンインターレースコンテナーデバイスクラスの定義](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-deinterlace-container-device-class)」および「[インターレース Bob デバイスクラスの定義](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-deinterlace-bob-device-class)」を参照してください。

 

 






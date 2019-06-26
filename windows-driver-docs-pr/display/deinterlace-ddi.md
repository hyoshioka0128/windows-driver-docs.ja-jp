---
title: デインターレース DDI
description: デインターレース DDI
ms.assetid: 06b85f76-950a-4a9b-af6b-ded823bfda6a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a79b7ba17b81f4556234ab8a6e6788709af06ad5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384898"
---
# <a name="deinterlace-ddi"></a>デインターレース DDI


## <span id="ddk_deinterlace_ddi_gg"></span><span id="DDK_DEINTERLACE_DDI_GG"></span>


ビデオ ミキシング レンダラー (VMR) は、インター レースを解除して、ビデオ コンテンツのフレーム レートの変換を実行できる、ように、ディスプレイ ドライバーが実装する必要があります、[補正コールバック関数のモーション](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

ドライバーの開発を簡略化するのには、モーション補正コード テンプレートを使用し、このセクションではデインター レース関数を実装します。 関数は、インター コンテナー デバイスまたはインター モードのデバイス クラスのいずれかのメンバー関数です。 詳細については、次を参照してください。[インター レースを解除するコンテナー デバイス クラスを定義する](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-deinterlace-container-device-class)と[インター レースを解除する Bob デバイス クラスを定義する](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-deinterlace-bob-device-class)します。

 

 






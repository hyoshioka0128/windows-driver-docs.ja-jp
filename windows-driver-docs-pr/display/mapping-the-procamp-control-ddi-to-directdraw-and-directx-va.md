---
title: DirectDraw を DirectX VA DDI ProcAmp コントロールをマップします。
description: DirectDraw から ProcAmp コントロール機能にアクセス[補正コールバック関数のモーション](motion-compensation-callbacks.md)にマップし、 [ProcAmp コントロール DDI](https://docs.microsoft.com/windows-hardware/drivers/display/procamp-control-ddi)します。
ms.assetid: ca2b92d9-7f3d-45b9-8841-43915dd4237d
keywords:
- ProcAmp WDK DirectX va なので、マッピング ProcAmp コントロール DDI
- マッピング ProcAmp コントロール DDI
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 30c01dbfdb3ac178e0ea0356a0e7661338447175
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370120"
---
# <a name="map-the-procamp-control-ddi-to-directdraw-and-directx-va"></a>DirectDraw を DirectX VA DDI ProcAmp コントロールをマップします。

ProcAmp コントロールの機能は、DirectDraw のを通じてアクセスする必要があります[補正コールバック関数のモーション](motion-compensation-callbacks.md)先、 [ProcAmp コントロール DDI](https://docs.microsoft.com/windows-hardware/drivers/display/procamp-control-ddi)マップすることができます。 DirectX の VA DDI を DirectDraw の動き補正コールバックにマップする方法の詳細については、次を参照してください。 [DirectDraw を DirectX VA インター レースを解除 DDI をマッピング](mapping-the-deinterlace-ddi-to-directdraw-and-directx-va.md)します。

次のトピックでは、モーションの補正コールバックに DDI ProcAmp コントロールをマップする方法について説明します。

[インター レース ProcAmp コントロールのコンテナーのデバイスを解除します。](deinterlace-container-device-for-procamp-control.md)

[ユーザー モード コンポーネントから DDI ProcAmp コントロールを呼び出す](calling-the-procamp-control-ddi-from-a-user-mode-component.md)

 

 






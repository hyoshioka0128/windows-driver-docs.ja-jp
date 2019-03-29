---
title: ProcAmp コントロール DDI
description: ProcAmp コントロール DDI
ms.assetid: 102e21eb-bad4-4ab5-8630-9ac37c33f20a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e77350d3e2f9f0d61a4caf5311ee5233dce2c8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573747"
---
# <a name="procamp-control-ddi"></a>ProcAmp コントロール DDI


## <span id="ddk_procamp_control_ddi_gg"></span><span id="DDK_PROCAMP_CONTROL_DDI_GG"></span>


ビデオの混在レンダラー (VMR) が ProcAmp コントロールの機能にアクセスできるように、ディスプレイ ドライバーが実装する必要があります、[補正コールバック関数のモーション](https://msdn.microsoft.com/library/windows/hardware/ff568441)します。

ドライバーの開発を簡略化するのには、動き補正コード テンプレートを使用し、このセクションでは ProcAmp コントロール関数を実装します。 関数は、インター コンテナー デバイスまたはデバイスの ProcAmp コントロール クラスのメンバー関数です。 詳細については、次を参照してください。[インター レースを解除するコンテナー デバイス クラスを定義する](https://msdn.microsoft.com/library/windows/hardware/ff552682)と[ProcAmp コントロール デバイス クラスを定義する](https://msdn.microsoft.com/library/windows/hardware/ff552686)します。

 

 






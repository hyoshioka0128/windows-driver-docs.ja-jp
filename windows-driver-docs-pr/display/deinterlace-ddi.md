---
title: DDI インター レースを解除します。
description: DDI インター レースを解除します。
ms.assetid: 06b85f76-950a-4a9b-af6b-ded823bfda6a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07a2aa7869adf9fdb6c3c9cd7aaa92eadfddaef6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558615"
---
# <a name="deinterlace-ddi"></a>DDI インター レースを解除します。


## <span id="ddk_deinterlace_ddi_gg"></span><span id="DDK_DEINTERLACE_DDI_GG"></span>


ビデオ ミキシング レンダラー (VMR) は、インター レースを解除して、ビデオ コンテンツのフレーム レートの変換を実行できる、ように、ディスプレイ ドライバーが実装する必要があります、[補正コールバック関数のモーション](https://msdn.microsoft.com/library/windows/hardware/ff568441)します。

ドライバーの開発を簡略化するのには、モーション補正コード テンプレートを使用し、このセクションではデインター レース関数を実装します。 関数は、インター コンテナー デバイスまたはインター モードのデバイス クラスのいずれかのメンバー関数です。 詳細については、次を参照してください。[インター レースを解除するコンテナー デバイス クラスを定義する](https://msdn.microsoft.com/library/windows/hardware/ff552682)と[インター レースを解除する Bob デバイス クラスを定義する](https://msdn.microsoft.com/library/windows/hardware/ff552679)します。

 

 






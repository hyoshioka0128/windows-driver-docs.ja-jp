---
title: 関数固有のインターフェイスの実装
description: 関数固有のインターフェイスの実装
ms.assetid: 6a15c8b5-17ca-4658-bf52-cf9b3307e706
keywords:
- オーディオミニポートドライバー WDK、ポートクラス
- ミニポートドライバー WDK オーディオ、ポートクラス
- ミニポートインターフェイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab1a400576228688e10321c72a64d4273e1709ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833255"
---
# <a name="implementation-of-function-specific-interfaces"></a>関数固有のインターフェイスの実装


## <span id="implementation_of_function_specific_interfaces"></span><span id="IMPLEMENTATION_OF_FUNCTION_SPECIFIC_INTERFACES"></span>


一般的なオーディオアダプターカードには、オーディオハードウェア関数のコレクションが含まれており、アダプタードライバーは、対応する IMiniport*Xxx*インターフェイスのコレクションを介して WDM オーディオシステムに公開できます。 すべての IMiniport*Xxx*インターフェイスは、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)から継承します。 各種類のミニポートインターフェイス (wave、MIDI、トポロジなど) は、アダプターカードの特定の種類のオーディオ機能を制御するためのミニポートドライバーをカプセル化します。 また、同じ (または同様の) ハードウェア関数の複数のインスタンスを表すために、ドライバーは同じミニポートインターフェイスの複数のインスタンスを公開することもできます。

詳細については、「[ミニポートインターフェイス](miniport-interfaces.md)」を参照してください。

 

 





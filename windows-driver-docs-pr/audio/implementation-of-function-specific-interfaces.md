---
title: 関数固有のインターフェイスの実装
description: 関数固有のインターフェイスの実装
ms.assetid: 6a15c8b5-17ca-4658-bf52-cf9b3307e706
keywords:
- オーディオのミニポート ドライバー WDK、ポート クラス
- ミニポート ドライバー WDK オーディオ、ポート クラス
- ミニポート インターフェイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c646dc9a6704081994cdbc3fa3226dfdcd4b7fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359939"
---
# <a name="implementation-of-function-specific-interfaces"></a>関数固有のインターフェイスの実装


## <span id="implementation_of_function_specific_interfaces"></span><span id="IMPLEMENTATION_OF_FUNCTION_SPECIFIC_INTERFACES"></span>


通常のオーディオ アダプター カード IMiniport の対応するコレクションを介して WDM オーディオ システムに公開できるアダプター ドライバー、オーディオ ハードウェア関数のコレクションを格納する*Xxx*インターフェイス。 すべての IMiniport*Xxx*インターフェイスを継承[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)します。 ミニポート インターフェイス--wave、MIDI、トポロジの各型し、ため on--特定の種類のアダプター カードのオーディオ機能を制御するためのミニポート ドライバーをカプセル化します。 ドライバーは、同じ (または同等) のハードウェア機能の複数のインスタンスを表すため、同じミニポート インターフェイスの複数のインスタンスを公開することもできます。

詳細については、次を参照してください。[ミニポート インターフェイス](miniport-interfaces.md)します。

 

 





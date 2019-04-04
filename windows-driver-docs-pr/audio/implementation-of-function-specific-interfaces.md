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
ms.openlocfilehash: 890d971a24494f14a2598046ae2b60221d6fc705
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582163"
---
# <a name="implementation-of-function-specific-interfaces"></a>関数固有のインターフェイスの実装


## <span id="implementation_of_function_specific_interfaces"></span><span id="IMPLEMENTATION_OF_FUNCTION_SPECIFIC_INTERFACES"></span>


通常のオーディオ アダプター カード IMiniport の対応するコレクションを介して WDM オーディオ システムに公開できるアダプター ドライバー、オーディオ ハードウェア関数のコレクションを格納する*Xxx*インターフェイス。 すべての IMiniport*Xxx*インターフェイスを継承[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)します。 ミニポート インターフェイス--wave、MIDI、トポロジの各型し、ため on--特定の種類のアダプター カードのオーディオ機能を制御するためのミニポート ドライバーをカプセル化します。 ドライバーは、同じ (または同等) のハードウェア機能の複数のインスタンスを表すため、同じミニポート インターフェイスの複数のインスタンスを公開することもできます。

詳細については、[ミニポート インターフェイス](miniport-interfaces.md)を参照してください。

 

 





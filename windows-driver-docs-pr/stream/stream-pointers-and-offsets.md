---
title: Stream ポインターとオフセット
description: Stream ポインターとオフセット
ms.assetid: ef9dc015-f0ee-49a6-8774-cfb0223c8b12
keywords:
- WDK AVStream、オフセットのポインターをストリーム配信します。
- WDK AVStream のオフセット
- ストリームは、WDK AVStream を配置します。
- 入力は、WDK AVStream を配置します。
- 出力は、WDK AVStream を配置します。
- AVStream ポインター WDK
- AVStream offsets WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83dd8c8a386ece90fc5b6ddbc06e49578c87ae1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560458"
---
# <a name="stream-pointers-and-offsets"></a>Stream ポインターとオフセット





A [ **KSSTREAM\_ポインター** ](https://msdn.microsoft.com/library/windows/hardware/ff567139)構造に含まれる 2 つ[ **KSSTREAM\_ポインター\_オフセット**](https://msdn.microsoft.com/library/windows/hardware/ff567140)フレーム内の入力と出力の位置のインデックスを作成できる構造体。 ミニドライバーでは、これらのオフセットを操作することまたは、フレームの解像度でデータにアクセスできます。

フレーム内のストリーム ポインターを進めるため、ミニドライバーを呼び出します[ **KsStreamPointerAdvanceOffsets** ](https://msdn.microsoft.com/library/windows/hardware/ff567126)と[ **KsStreamPointerAdvanceOffsetsAndUnlock**](https://msdn.microsoft.com/library/windows/hardware/ff567127).

仮想アドレスを含むストリームのデータにアクセスするミニドライバーは、これらのオフセットを使用して、バイトの解像度でストリームの位置を指定します。 スキャッター/ギャザーの物理的なマッピングを使用するミニドライバーは、粒度でストリームの位置を指定できます、 [ **KSMAPPING** ](https://msdn.microsoft.com/library/windows/hardware/ff563394)構造体。

 

 





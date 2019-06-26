---
title: ストリーム ポインターとオフセット
description: ストリーム ポインターとオフセット
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
ms.openlocfilehash: 9831c5d658131c8e628d0110656fa6e479824fff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377796"
---
# <a name="stream-pointers-and-offsets"></a>ストリーム ポインターとオフセット





A [ **KSSTREAM\_ポインター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksstream_pointer)構造に含まれる 2 つ[ **KSSTREAM\_ポインター\_オフセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksstream_pointer_offset)フレーム内の入力と出力の位置のインデックスを作成できる構造体。 ミニドライバーでは、これらのオフセットを操作することまたは、フレームの解像度でデータにアクセスできます。

フレーム内のストリーム ポインターを進めるため、ミニドライバーを呼び出します[ **KsStreamPointerAdvanceOffsets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsets)と[ **KsStreamPointerAdvanceOffsetsAndUnlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock).

仮想アドレスを含むストリームのデータにアクセスするミニドライバーは、これらのオフセットを使用して、バイトの解像度でストリームの位置を指定します。 スキャッター/ギャザーの物理的なマッピングを使用するミニドライバーは、粒度でストリームの位置を指定できます、 [ **KSMAPPING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksmapping)構造体。

 

 





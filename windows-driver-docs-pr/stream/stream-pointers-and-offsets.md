---
title: ストリーム ポインターとオフセット
description: ストリーム ポインターとオフセット
ms.assetid: ef9dc015-f0ee-49a6-8774-cfb0223c8b12
keywords:
- ストリームポインター WDK AVStream、オフセット
- WDK AVStream をオフセットする
- ストリームの位置 WDK AVStream
- 入力位置 WDK AVStream
- 出力位置 WDK AVStream
- AVStream ポインター WDK
- AVStream オフセット WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c76a994350d09af95a2a3f2183cc93a2640c4b16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837675"
---
# <a name="stream-pointers-and-offsets"></a>ストリーム ポインターとオフセット





[**Ksk ストリーム\_ポインター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)構造体には、フレーム内の入力および出力位置にインデックスを作成する2つの[**KSK ストリーム\_ポインター\_オフセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer_offset)構造体が含まれています。 ミニドライバーは、これらのオフセットを操作するか、フレーム解像度でデータにアクセスすることができます。

フレーム内のストリームポインターを進めるには、ミニドライバーは[**KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)と[**KsStreamPointerAdvanceOffsetsAndUnlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock)を呼び出します。

仮想アドレスを持つストリームデータにアクセスするミニドライバーは、これらのオフセットを使用して、バイト解像度でストリームの位置を指定できます。 スキャッター/gather 物理マッピングを使用するミニドライバーでは、ストリームの位置を[**Ksmapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksmapping)構造の粒度で指定できます。

 

 





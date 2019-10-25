---
title: AVStream コーデックでのストリームの終わりの処理
description: AVStream コーデックでのストリームの終わりの処理
ms.assetid: ee57137b-999a-449f-9f9d-50bc19e07ba8
keywords:
- ストリームの最後の WDK AVStream の処理
- ストリームの終わり WDK AVStream
- ハードウェアコーデックサポート WDK AVStream、ストリームの終了
- AVStream ハードウェアコーデックサポート WDK、ストリームの終端の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c98259e9d7399fe611cca46ffb59bfc800bb814
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838087"
---
# <a name="handling-end-of-stream-in-avstream-codecs"></a>AVStream コーデックでのストリームの終わりの処理


HW MFT が、ストリームの終わり (EOS) フラグが設定されたサンプルを受け取ると、そのサンプルに対応する[**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造の**optionsflag**メンバーで、ksstream\_header\_オプション sf\_endofstream に設定されます.

ミニドライバーは、KSK ストリームを使用して[**ksk\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)を受信した後、\_ヘッダー\_optionsf\_endofstream フラグを**streamheader. フラグ**で設定した後、入力ピンは新しい入力ストリームポインターを受信しなくなります。ミニドライバーは、出力ストリームポインターに対して KSK ストリーム\_ヘッダー\_オプション SF\_ENDOFSTREAM を設定します。

ミニドライバーが KSK ストリーム\_ヘッダー\_\_オプションを設定する前に、出力ストリームポインターで ENDOFSTREAM を指定すると、現在使用可能な入力値でできるだけ多くの出力フレームが生成されます。

ミニドライバーは、これらのストリームポインターに関連付けられているデータに加えて、以前に処理されたストリームポインターに関連するキャッシュされた情報をクリアする必要があります。 次に、ミニドライバーは、出力ピンに KSK ストリーム\_ヘッダー\_オプション SF\_ENDOFSTREAM を設定する必要があります。

ミニドライバーは、後で新しいストリームの一部として到着する新しい入力ストリームポインターを処理する必要があります。 例外は、メディアストリームの不連続性の結果として EOS が発生した場合です。 この場合、新しく到着したストリームポインターには、KSK ストリーム\_ヘッダー\_オプション SF\_DATADISCONTINUITY または KSSTREAM\_ヘッダー\_オプション SF\_TIMEDISCONTINUITY 性、またはその両方が KSK ストリームに設定されています\_項目.**オプションフラグ**。 これらのフラグが設定されているストリームポインターが入力ピンに到達した場合、ミニドライバーは、対応する出力ピンのストリームポインターに同じフラグを設定する必要があります。

 

 





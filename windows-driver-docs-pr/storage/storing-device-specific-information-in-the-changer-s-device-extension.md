---
title: チェンジャーのデバイス拡張へのデバイス固有情報の格納
description: チェンジャーのデバイス拡張へのデバイス固有情報の格納
ms.assetid: 72048d84-1c2d-4f3c-b5e8-f55a812ad567
keywords:
- チェンジャードライバー WDK storage、デバイス固有のデータストレージ
- ストレージチェンジャードライバー WDK、デバイス固有のデータストレージ
- デバイス固有のデータストレージ WDK チェンジャー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05ed58571c32b7949d1645007654226351a615e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844462"
---
# <a name="storing-device-specific-information-in-the-changers-device-extension"></a>チェンジャーのデバイス拡張へのデバイス固有情報の格納


## <span id="ddk_storing_device_specific_information_in_the_changers_device_extensi"></span><span id="DDK_STORING_DEVICE_SPECIFIC_INFORMATION_IN_THE_CHANGERS_DEVICE_EXTENSI"></span>


チェンジャー miniclass ドライバーは、 [**Changeradditionalextensionsize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changeradditionalextensionsize)ルーチン内のデバイス固有のデータに必要なストレージを指定します。 チェンジャークラスドライバーは、要求された記憶域をチェンジャー miniclass ドライバーの代わりに割り当て、miniclass ドライバーの[**Changerinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerinitialize)ルーチンを呼び出します。

チェンジャー miniclass ドライバーがデバイス拡張機能にデータを格納するかどうかと、格納されるデータは、ドライバーデザイナーによって決まります。 これには通常、チェンジャーデバイスと同等の SCSI 問い合わせデータや SCSI 以外のものが含まれます。

デバイス拡張機能には、miniclass ドライバーがデバイス固有の要素アドレスと、要求で渡された0から始まる要素アドレスとの間で変換を行うために使用するデータが含まれる場合もあります。 要求では、要素は、指定された型の最初の要素の0から始まる要素型によってアドレス指定されます。 通常、デバイス固有のアドレスは、この要素のアドレス指定スキームに従っていないため、チェンジャー miniclass ドライバーは、受信した0から始まる要素アドレスをデバイス固有の要素アドレスに変換する必要があります。

アドレスが翻訳されている限り、miniclass ドライバーが要素アドレスをどのように変換するかは関係ありません。 プロセスを最適化するために、miniclass ドライバーは、デバイス拡張機能での翻訳を促進するデータを格納する場合があります。 たとえば、初期化時に、ドライバーは SCSI 要素のアドレス割り当てページまたは非 SCSI 対応のデバイス固有の要素アドレスを取得し、デバイス固有のアドレスを再構築するために使用できるオフセットにマップし、デバイス拡張機能でオフセットします。 次に、チェンジャー miniclass ドライバーが、0から始まる要素アドレスを含む要求を受信すると、デバイス拡張機能に格納されているオフセットを使用して、0から始まるアドレスをデバイス固有の同等のアドレスに変換できます。 チェンジャー miniclass ドライバーは、システムポートドライバーに送信される SRBs でこれらのデバイス固有のアドレスを使用できます。

 

 





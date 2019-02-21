---
title: チェンジャーのデバイスの拡張機能にデバイスに固有の情報を格納します。
description: チェンジャーのデバイスの拡張機能にデバイスに固有の情報を格納します。
ms.assetid: 72048d84-1c2d-4f3c-b5e8-f55a812ad567
keywords:
- チェンジャー ドライバー WDK のストレージ、デバイスに固有のデータ ストレージ
- 記憶域チェンジャー ドライバー WDK、デバイスに固有のデータ ストレージ
- デバイスに固有のデータ ストレージの WDK チェンジャー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38ed70319bd7c22cc20044f0a63296e6538674b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536060"
---
# <a name="storing-device-specific-information-in-the-changers-device-extension"></a>チェンジャーのデバイスの拡張機能にデバイスに固有の情報を格納します。


## <span id="ddk_storing_device_specific_information_in_the_changers_device_extensi"></span><span id="DDK_STORING_DEVICE_SPECIFIC_INFORMATION_IN_THE_CHANGERS_DEVICE_EXTENSI"></span>


チェンジャー miniclass ドライバーがデバイスに固有のデータの必要なストレージを指定します、 [ **ChangerAdditionalExtensionSize** ](https://msdn.microsoft.com/library/windows/hardware/ff551400)ルーチン。 チェンジャー クラス ドライバーに代わってチェンジャー miniclass ドライバーでは、要求されたストレージが割り当てられ、miniclass ドライバーの[ **ChangerInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff551431)ルーチン。

チェンジャー miniclass ドライバーがデバイスの拡張機能にデータを格納するかどうかとどのようなデータを格納、ドライバーのデザイナーの責任です。 通常、SCSI 問い合わせデータまたはチェンジャー デバイスの SCSI 非同等を掲載しています。

デバイスの拡張機能は、デバイス固有の要素のアドレスとの要求で渡された要素の 0 から始まるアドレス間で変換を miniclass ドライバーを使用するデータもあります。 要求では、要素は要素の種類を使用して、指定された型の最初の要素の 0 から始まるによってアドレス指定します。 デバイスに固有のアドレス通常に従っていないこの要素のアドレス指定スキームようにチェンジャー miniclass ドライバーがデバイスに固有の要素のアドレスを受け取る要素の 0 から始まるアドレスに変換する必要があります。

アドレスは、変換としてに miniclass ドライバーが要素のアドレスに変換する方法もかまいません。 プロセスを最適化するには、miniclass ドライバーは、デバイスの拡張機能で変換を容易にするデータを格納可能性があります。 たとえばの初期化で、ドライバーでしたから、SCSI 要素のアドレスの割り当て ページまたは SCSI 非同等のデバイス固有の要素のアドレスを取得、および格納する、デバイスに固有のアドレスを再構築に使用できるオフセットにマップしますデバイスの拡張機能内のオフセット。 次に、チェンジャー miniclass ドライバーでは、0 から始まる要素のアドレスを含む要求を受信したときに、デバイス固有の値を 0 から始まるアドレスに変換するのにデバイスの拡張機能に格納されたオフセットを使用できます。 チェンジャー miniclass ドライバーでは、システム ポート ドライバーに送信される Srb でこれらのデバイスに固有のアドレスを使用できます。

 

 





---
title: 動的なオーディオ サブデバイスのジャックに関する説明
description: 動的なオーディオ サブデバイスのジャックに関する説明
ms.assetid: e04f4000-3b93-4f4b-afec-007e5821f125
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2d8c2b763f60ac4fbb9542320daf1399cfa0bfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359837"
---
# <a name="jack-descriptions-for-dynamic-audio-subdevices"></a>動的なオーディオ サブデバイスのジャックに関する説明


Windows Vista 以降では、 [ **KSPROPERTY\_ジャック\_説明**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)プロパティでオーディオのアダプターでのサブデバイスについては、回線のモジュラー ジャックまたはジャックのコレクションを提供します。 (このコンテキストで、用語*サブデバイス*は同義です*KS フィルター*)。プロパティの値は 1 つまたは複数の配列[ **KSJACK\_説明**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)構造体。 各構造体には、色、コネクタの種類、および、ジャックの物理的な場所について説明します。 さらに、構造に含まれる、 **IsConnected**メンバーである**TRUE**場合は、マイク、ヘッドホンなど、オーディオ エンドポイント デバイス、ジャックに接続されている、 **FALSE**ジャックが空の場合。 最新の値を提供する**IsConnected**アダプターのドライバーを動的サブデバイスはオーディオ ハードウェアのジャック プレゼンス検出機能を利用します。 (なしのジャック プレゼンスの検出の)、静的サブデバイスの**IsConnected**メンバーは常に**TRUE**します。 詳細については、次を参照してください。[ジャックの Description プロパティ](jack-description-property.md)します。

動的サブデバイスのジャックにプラグを挿入すると、アダプターのドライバーで呼び出す必要があります、 [ **PcRegisterSubdevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregistersubdevice)サブデバイスを登録する関数。 アダプター ドライバーが受信、IOCTL、KSPROPERTY を格納している場合に、サブデバイスが登録されている間\_ジャック\_ドライバーを設定する必要があります、サブデバイスの説明を要求、 **IsConnected**のメンバープロパティの値を**TRUE**します。

アダプタのドライバを呼び出す必要があります、ユーザーは、動的サブデバイスのジャックからプラグを削除するとき、 [ **IUnregisterSubdevice::UnregisterSubdevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice)サブデバイスの登録を削除するメソッド。 サブデバイス、登録されていないアダプター ドライバーが受信、IOCTL、KSPROPERTY を格納している場合、\_ジャック\_ドライバーを設定する必要があります、サブデバイスの説明を要求、 **IsConnected**のメンバー、プロパティの値を**FALSE**します。

 

 





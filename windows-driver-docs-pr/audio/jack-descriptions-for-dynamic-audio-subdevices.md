---
title: 動的なオーディオ サブデバイス ジャックの説明
description: 動的なオーディオ サブデバイス ジャックの説明
ms.assetid: e04f4000-3b93-4f4b-afec-007e5821f125
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 071116f3e455f4d61e0653c0a986f1d3732aa908
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553106"
---
# <a name="jack-descriptions-for-dynamic-audio-subdevices"></a>動的なオーディオ サブデバイス ジャックの説明


Windows Vista 以降では、 [ **KSPROPERTY\_ジャック\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)プロパティでオーディオのアダプターでのサブデバイスについては、回線のモジュラー ジャックまたはジャックのコレクションを提供します。 (このコンテキストで、用語*サブデバイス*は同義です*KS フィルター*)。プロパティの値は 1 つまたは複数の配列[ **KSJACK\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537136)構造体。 各構造体には、色、コネクタの種類、および、ジャックの物理的な場所について説明します。 さらに、構造に含まれる、 **IsConnected**メンバーである**TRUE**場合は、マイク、ヘッドホンなど、オーディオ エンドポイント デバイス、ジャックに接続されている、 **FALSE**ジャックが空の場合。 最新の値を提供する**IsConnected**アダプターのドライバーを動的サブデバイスはオーディオ ハードウェアのジャック プレゼンス検出機能を利用します。 (なしのジャック プレゼンスの検出の)、静的サブデバイスの**IsConnected**メンバーは常に**TRUE**します。 詳細については、次を参照してください。[ジャックの Description プロパティ](jack-description-property.md)します。

動的サブデバイスのジャックにプラグを挿入すると、アダプターのドライバーで呼び出す必要があります、 [ **PcRegisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537731)サブデバイスを登録する関数。 アダプター ドライバーが受信、IOCTL、KSPROPERTY を格納している場合に、サブデバイスが登録されている間\_ジャック\_ドライバーを設定する必要があります、サブデバイスの説明を要求、 **IsConnected**のメンバープロパティの値を**TRUE**します。

アダプタのドライバを呼び出す必要があります、ユーザーは、動的サブデバイスのジャックからプラグを削除するとき、 [ **IUnregisterSubdevice::UnregisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537032)サブデバイスの登録を削除するメソッド。 サブデバイス、登録されていないアダプター ドライバーが受信、IOCTL、KSPROPERTY を格納している場合、\_ジャック\_ドライバーを設定する必要があります、サブデバイスの説明を要求、 **IsConnected**のメンバー、プロパティの値を**FALSE**します。

 

 





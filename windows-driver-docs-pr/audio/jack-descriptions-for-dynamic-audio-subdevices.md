---
title: 動的なオーディオ サブデバイスのジャックに関する説明
description: 動的なオーディオ サブデバイスのジャックに関する説明
ms.assetid: e04f4000-3b93-4f4b-afec-007e5821f125
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7cfbfc4dbbd85a324181367d582ca5c0e84965f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833194"
---
# <a name="jack-descriptions-for-dynamic-audio-subdevices"></a>動的なオーディオ サブデバイスのジャックに関する説明


Windows Vista 以降では、 [**Ksk プロパティ\_jack\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)プロパティは、オーディオアダプターのサブデバイス上のジャックまたはジャックのコレクションに関する情報を提供します。 (このコンテキストでは、 *subdevice*という用語は*KS フィルター*と同義です)。プロパティ値は、1つ以上の[**Ksk ジャック\_記述**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)構造体の配列です。 各構造体には、ジャックの色、コネクタの種類、および物理的な位置が記述されています。 また、この構造体には**IsConnected**メンバーが含まれています。これは、マイクやヘッドホンなどのオーディオエンドポイントデバイスがジャックに接続されている場合は**TRUE** 、ジャックが空の場合は**FALSE**です。 **IsConnected**の最新の値を提供するために、動的サブデバイスのアダプタードライバーは、オーディオハードウェアのジャックプレゼンス検出機能に依存しています。 (ジャックの有無を検出せずに) 静的サブデバイスの場合、 **IsConnected**メンバーは常に**TRUE**である必要があります。 詳細については、「 [Jack Description プロパティ](jack-description-property.md)」を参照してください。

ユーザーが動的サブデバイスのジャックにプラグインを挿入すると、アダプタードライバーは、サブデバイスを登録するために、 [**Pcregiのサブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)デバイス関数を呼び出す必要があります。 サブデバイスが登録されたままになっている間に、アダプタードライバーが、サブデバイスの\_ジャック\_DESCRIPTION 要求を含む IOCTL を受信した場合、ドライバーはプロパティ値の**IsConnected**メンバーを**TRUE**に設定する必要があります.

ユーザーが動的サブデバイスのジャックからプラグを削除すると、アダプタードライバーは[**Iunregistersubdevice:: unregistersubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice)メソッドを呼び出して、サブデバイスの登録を削除する必要があります。 サブデバイスが登録されていない場合、アダプタードライバーは、KSK プロパティ\_JACK\_DESCRIPTION 要求を含む IOCTL をサブデバイスに対して受信すると、プロパティ値の**IsConnected**メンバーを**FALSE**に設定する必要があります。

 

 





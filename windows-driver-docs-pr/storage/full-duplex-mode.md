---
title: 全二重モード
description: 全二重モード
ms.assetid: 01e3388d-d568-4476-9ff0-2125acafb841
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1532059d7feb3a1f412c8f4893aa83e8497aef60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378560"
---
# <a name="full-duplex-mode"></a>全二重モード


## <span id="ddk_full_duplex_mode_kg"></span><span id="DDK_FULL_DUPLEX_MODE_KG"></span>


Storport ドライバーには、高パフォーマンスのバスに特化した I/O モデルをサポートしています。 この I/O モデルでは、ミニポート ドライバーに追加、新しい要求がキュー場合でも、他のユーザーの完了の場合は、つまり、全二重モードで動作するミニポート ドライバーを許可します。 さらに、全二重モード、ミニポート ドライバーがの実行を同期するその[ **StartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)割り込みサービス ルーチンとします。 これは、大幅なパフォーマンスの向上につながります。 ただし、Storport は、既定では、半二重モードで動作するためのミニポート ドライバーを全二重モードで活用するために設計する必要があります。

ミニポート ドライバーが Storport の実行中に、全二重モードで動作するを構成する必要があります、 [ **HwStorFindAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)ルーチン。 これは、初期化して、 **SynchronizationModel**のミニポート ドライバーのメンバー [**ポート\_構成\_情報 (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))構造体を**StorSynchronizeFullDuplex**します。

 

 





---
title: 全二重モード
description: 全二重モード
ms.assetid: 01e3388d-d568-4476-9ff0-2125acafb841
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2edef06203a4e9efec7f06244867ebd83186c36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843405"
---
# <a name="full-duplex-mode"></a>全二重モード


## <span id="ddk_full_duplex_mode_kg"></span><span id="DDK_FULL_DUPLEX_MODE_KG"></span>


Storport ドライバーでは、高パフォーマンスのバス専用に調整された i/o モデルがサポートされています。 この i/o モデルを使用すると、ミニポートドライバーを全二重モードで動作させることができます。つまり、ミニポートドライバーは、他のユーザーの完了処理中でも、新しい要求をキューに追加できます。 さらに、全二重モードでは、ミニポートドライバーは、 [**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)および interrupt サービスルーチンの実行を同期する必要はありません。 これにより、パフォーマンスが大幅に向上する可能性があります。 ただし、Storport は、既定ではハーフデュプレックスモードで動作するため、全二重モードを利用するようにミニポートドライバーを設計する必要があります。

ミニポートドライバーは、 [**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)ルーチンの実行中に全二重モードで動作するように Storport を構成する必要があります。 これを行うには、ミニポートドライバーの[**ポート\_CONFIGURATION\_INFORMATION (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))構造体の**同期モデル**メンバーを**StorSynchronizeFullDuplex**に初期化します。

 

 





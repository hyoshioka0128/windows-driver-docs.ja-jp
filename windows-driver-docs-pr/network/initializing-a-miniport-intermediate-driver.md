---
title: ミニポート中間ドライバーの初期化
description: ミニポート中間ドライバーの初期化
ms.assetid: b0beea1f-7374-49e9-9650-0bdb37902469
keywords:
- NDIS 中間ドライバー WDK、初期化中
- 中間ドライバー WDK ネットワーク、初期化
- ミニポート-中間ドライバーの初期化
- ミニポート-中間ドライバー WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 057230284757b87e77fe7c174904155718fe5892
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824503"
---
# <a name="initializing-a-miniport-intermediate-driver"></a>ミニポート中間ドライバーの初期化





ミニポート中間ドライバーは、仮想デバイス用のミニポートドライバー、プロトコルドライバー、および物理デバイス用のミニポートドライバーを結合します。 ミニポート中間ドライバーは、ミニポートドライバーに階層化された中間ドライバーと同様に機能します。 このようなドライバーを使用すると、中間ドライバーは、2つの異なるドライバーを使用した場合にパフォーマンスの低下を招くことなく、基になるミニポートドライバーと直接通信することができます。

物理ミニポートドライバーを登録するために、ミニポート中間ドライバーは、任意のミニポートドライバーと同様に、適切なパラメーターを使用して[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数を呼び出します。 仮想ミニポートを登録するために、ドライバーは**NdisMRegisterMiniportDriver**を再度呼び出しますが、NDIS\_中間\_ドライバーフラグを*Miniportdrivercharacteristics*の構造体に設定します。

ミニポート中間ドライバーの仮想または物理デバイスインスタンスごとに、 **Imminiport ポート**レジストリキーが**DWORD: 0x0000001**に設定されている場合、NDIS は、ドライバーによって仮想マシンに登録された[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出します。ドライブ. それ以外の場合、NDIS はドライバーによって物理デバイスに登録されたドライバーの*MiniportInitializeEx*関数を呼び出します。

 

 






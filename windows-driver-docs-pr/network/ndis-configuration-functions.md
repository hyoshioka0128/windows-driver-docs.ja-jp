---
title: NDIS 構成関数
description: NDIS 構成関数
ms.assetid: 248e08d0-6145-499a-b307-2a5ffbd3733f
keywords:
- WDK NDIS の構成関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44a4e5f4e5e40654d72392f7d0e307330346a3bd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383601"
---
# <a name="ndis-configuration-functions"></a>NDIS 構成関数





NDIS にはドライバーの構成を簡略化するには、次の関数が含まれています。

[**NdisOpenConfigurationEx**](https://msdn.microsoft.com/library/windows/hardware/ff563717)

[**NdisMGetBusData**](https://msdn.microsoft.com/library/windows/hardware/ff563591)

[**NdisMSetBusData**](https://msdn.microsoft.com/library/windows/hardware/ff563670)

NDIS ミニポート ドライバーを呼び出し、アダプターの構成情報を取得する**NdisOpenConfigurationEx**と[**エミュレーター**](https://msdn.microsoft.com/library/windows/hardware/ff564511)します。 ドライバーを呼び出すことができます**NdisMGetBusData** bus 固有の情報を取得します。 ドライバーを呼び出すことができます**NdisMSetBusData** bus 固有の情報を設定します。

プロトコル ドライバーでは、アダプターの名前へのレジストリ パスを使用して、ドライバーと基になるアダプター間のバインディングに固有の構成パラメーターを読み取ります。 NDIS への呼び出しで、レジストリ パスを提供する、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数。 ドライバーは、このレジストリ パスを渡すことができます、 [ **NdisOpenProtocolConfiguration** ](https://msdn.microsoft.com/library/windows/hardware/ff553683)関数またはレジストリを直接呼び出します。 代わりに、ドライバーを渡すことができます、 *BindParameters*構造体を**NdisOpenConfigurationEx**を同じパラメーターを読み取る関数。

 

 






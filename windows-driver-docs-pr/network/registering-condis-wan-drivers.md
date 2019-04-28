---
title: CoNDIS WAN ドライバーの登録
description: CoNDIS WAN ドライバーの登録
ms.assetid: e699d1b0-9dbd-4845-b8e3-e83da20e997c
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、登録します。
- NdisMRegisterMiniportDriver
- 登録している CoNDIS WAN ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0ae782bce2b9fa27523ae908308932ab8004012
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364070"
---
# <a name="registering-condis-wan-drivers"></a>CoNDIS WAN ドライバーの登録





呼び出しいる CoNDIS WAN ミニポート ドライバーまたは MCM [ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)からその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)を登録する関数、標準*MiniportXxx* NDIS 関数。 登録の詳細については*MiniportXxx*関数を参照してください[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

いる CoNDIS WAN コール マネージャーは、NDIS プロトコル ドライバーです。 コール マネージャーは、そのため、 [ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)その標準を登録する*ProtocolXxx*関数。 NDIS プロトコル ドライバーの登録の詳細については、次を参照してください。[プロトコル ドライバーの初期化](initializing-a-protocol-driver.md)します。 その他のコール マネージャーの初期化と MCM の初期化の違いについては、次を参照してください。[初期化の相違](differences-in-initialization.md)します。

呼び出し**NdisMRegisterMiniportDriver**提供、NDIS\_ミニポート\_ドライバー\_ミニポート ドライバーからの特性構造体。 正しい NDIS バージョン番号を指定する必要があります。 NDIS バージョン番号を設定する方法についての詳細については、次を参照してください。 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)します。

いる CoNDIS WAN ドライバーは、NDIS version 5.0 以降に示す必要があります。

NDIS 6.0 とそれ以降のドライバーする必要がありますいる CoNDIS コールバック関数よう登録。

-   いる CoNDIS を登録する*ProtocolXxx*と*MiniportXxx*いる CoNDIS のすべてのドライバーを呼び出す必要があります、関数、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数。

-   そのいる CoNDIS を登録する*MiniportXxx*関数、ミニポート ドライバーまたはミニポート コール マネージャー (MCM) を呼び出す必要があります、 **NdisSetOptionalHandlers**関数からその[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数を渡して、 [ **NDIS\_ミニポート\_CO\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565948)構造体。 コール マネージャーを登録する*ProtocolXxx*関数、MCMs も提供、 [ **NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー** ](https://msdn.microsoft.com/library/windows/hardware/ff564883)構造体。

-   そのいる CoNDIS を登録する*ProtocolXxx*関数、クライアントまたは呼び出しのマネージャーを呼び出す必要があります、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数からその[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)関数を提供する必要があります、 [ **NDIS\_プロトコル\_CO\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566817)構造体。 クライアントを提供する必要がありますも、 [ **NDIS\_CO\_クライアント\_(省略可能)\_ハンドラー** ](https://msdn.microsoft.com/library/windows/hardware/ff564884)構造と呼び出しのマネージャーでは、を提供する必要がありますも[ **NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー** ](https://msdn.microsoft.com/library/windows/hardware/ff564883)構造体。

いる CoNDIS ドライバーの登録の詳細については、次を参照してください。[いる CoNDIS 登録](condis-registration.md)します。

.

 

 






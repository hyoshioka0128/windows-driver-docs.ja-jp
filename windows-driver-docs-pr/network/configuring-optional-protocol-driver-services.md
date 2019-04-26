---
title: オプションのプロトコル ドライバー サービスの構成
description: オプションのプロトコル ドライバー サービスの構成
ms.assetid: 3bb6d0ed-bc44-48c6-8f28-d861c4ff7a87
keywords:
- プロトコル ドライバー WDK、省略可能なネットワーク サービス
- NDIS プロトコル ドライバー WDK、省略可能なサービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 038ef1eaf48247d5f723ba837c720ed43eda605a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357438"
---
# <a name="configuring-optional-protocol-driver-services"></a>オプションのプロトコル ドライバー サービスの構成





NDIS 呼び出しプロトコル ドライバーの[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)省略可能なサービスを構成するプロトコルのドライバーを許可する関数。 NDIS 呼び出し*ProtocolSetOptions*プロトコル ドライバーの呼び出しのコンテキスト内で、 [ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)関数

*ProtocolSetOptions*レジスタのエントリ ポイントの既定オプション*ProtocolXxx*関数およびその他のドライバー リソースを割り当てることができます。 省略可能な登録*ProtocolXxx*関数、プロトコルのドライバーの呼び出し、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数をある特性構造体を渡します、*OptionalHandlers*パラメーター。 この場合、プロトコル ドライバーに渡しますからハンドル、 *NdisDriverHandle*パラメーターの*ProtocolSetOptions*で、 *NdisHandle*パラメーターの**NdisSetOptionalHandlers**します。

プロトコル ドライバーを呼び出すことも**NdisSetOptionalHandlers**から、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数または[ *ProtocolOpenAdapterCompleteEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570265)プロトコル ドライバーがある有効なハンドルから後、機能、 [ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715)関数。 この場合、プロトコル ドライバーに渡しますからハンドル、 *NdisBindingHandle*パラメーターの**NdisOpenAdapterEx**で、 *NdisHandle*パラメーターの**NdisSetOptionalHandlers**します。

この場合は、有効な特性構造体には。

[**NDIS\_プロトコル\_CO\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566817)

[**NDIS\_CO\_クライアント\_(省略可能)\_ハンドラー**](https://msdn.microsoft.com/library/windows/hardware/ff564884)

[**NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー**](https://msdn.microsoft.com/library/windows/hardware/ff564883)

NDIS\_クライアント\_CHIMNEY\_オフロード\_ジェネリック\_特性 (を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))

NDIS\_クライアント\_CHIMNEY\_オフロード\_TCP\_特性 (を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))

 

 






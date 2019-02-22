---
title: 省略可能なミニポート ドライバー サービスを構成します。
description: 省略可能なミニポート ドライバー サービスを構成します。
ms.assetid: 42fe3863-ded0-4a02-9216-86fa4c167a49
keywords:
- ミニポート ドライバー WDK、省略可能なネットワーク サービス
- NDIS ミニポート ドライバー WDK、省略可能なサービス
- MiniportSetOptions
- 特性構造の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32acf87c53e965d4144c372286e886592680dd73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558098"
---
# <a name="configuring-optional-miniport-driver-services"></a>省略可能なミニポート ドライバー サービスを構成します。





NDIS ミニポート ドライバーを呼び出す[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)省略可能なサービスを構成するドライバーを許可する関数。 NDIS 呼び出し*MiniportSetOptions*ミニポート ドライバーの呼び出しのコンテキスト内で、 [ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)関数。

*MiniportSetOptions*の既定のエントリ ポイントを登録します。 省略可能な*MiniportXxx*関数およびその他のドライバー リソースを割り当てることができます。 省略可能な登録*MiniportXxx*関数、ミニポート ドライバーの呼び出し、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数をある特性構造体を渡します、*OptionalHandlers*パラメーター。

NDIS 6.0 以降では、有効な特性構造体以下に示します。

[**NDIS\_ミニポート\_CO\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565948)

[**NDIS\_ミニポート\_PNP\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566475)

[**NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー**](https://msdn.microsoft.com/library/windows/hardware/ff564883)

[**NDIS\_プロバイダー\_CHIMNEY\_オフロード\_ジェネリック\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566846) (を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))

[**NDIS\_プロバイダー\_CHIMNEY\_オフロード\_TCP\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566852) (を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))

NDIS 6.30 以降では、有効な特性構造も次に示します。

[**NDIS\_ミニポート\_SS\_特性**](https://msdn.microsoft.com/library/windows/hardware/hh451559)

[**NDIS\_NDK\_プロバイダー\_特性**](https://msdn.microsoft.com/library/windows/hardware/hh451566)

 

 






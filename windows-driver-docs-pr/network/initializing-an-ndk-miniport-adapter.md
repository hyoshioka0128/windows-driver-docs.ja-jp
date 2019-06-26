---
title: NDK ミニポート アダプターの初期化
description: このセクションは、NDK ミニポート アダプターを初期化する方法を説明します
ms.assetid: 0A920057-3C12-4770-BA08-6C3BB24072EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cdec770f7ef7b92df0c10dbfc8a9034247c0df1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381294"
---
# <a name="initializing-an-ndk-miniport-adapter"></a>NDK ミニポート アダプターの初期化


Network Direct カーネル (NDK) ミニポート アダプターは、他のミニポート アダプターと同じ方法で初期化されます。NDIS ミニポート アダプターの呼び出す[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)で説明されているとおりに機能[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。 このトピックでは、ミニポート アダプターの NDK に固有の要件を説明します。 *MiniportInitializeEx*関数。

その[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数、ミニポート ドライバーは、次を実行する必要があります。

1.  設定、 [ **NDIS\_ミニポート\_アダプター\_NDK\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_ndk_attributes)次のように、アダプターの構造体します。

    - ミニポート ドライバーのセット、**ヘッダー** NDK 対応ミニポート アダプターとしてアダプターを識別するためにメンバーをメンバーの説明で説明されているとします。

    - ミニポート ドライバーのセット、**有効**メンバー **TRUE** NDK 機能が有効になっている場合または**FALSE**それ以外の場合。

        > [!NOTE]
        > クエリを実行して、ミニポート ドライバーの NDK 機能の現在の状態の設定の詳細については、次を参照してください。 [NDK 機能の無効化の有効化と](enabling-and-disabling-ndk-functionality.md)します。         

    - **NdkCapabilities**メンバーへのポインターを格納するミニポート ドライバー、 [ **NDIS\_NDK\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_capabilities)構造体を指定します。アダプターの機能です。

2.  呼び出す[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)アダプターのこれらの属性を設定します。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 







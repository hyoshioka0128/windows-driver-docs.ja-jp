---
title: NDK ミニポート アダプターの初期化
description: このセクションでは、NDK ミニポートアダプターを初期化する方法について説明します。
ms.assetid: 0A920057-3C12-4770-BA08-6C3BB24072EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06b4c8bd7cc6d96073bc145b36fe032f960da97b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824493"
---
# <a name="initializing-an-ndk-miniport-adapter"></a>NDK ミニポート アダプターの初期化


ネットワークダイレクトカーネル (NDK) ミニポートアダプターは、他のミニポートアダプターと同じ方法で初期化されます。 NDIS は、「[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)」で説明されているように、ミニポートアダプターの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出します。 このトピックでは、ミニポートアダプターの*MiniportInitializeEx*関数の NDK 固有の要件について説明します。

[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数では、ミニポートドライバーは次の操作を行う必要があります。

1.  次の手順に従って、 [**NDIS\_ミニポート\_アダプター\_NDK\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_ndk_attributes)構造体に設定します。

    - ミニポートドライバーは、「メンバーの説明」で説明されているように**ヘッダー**メンバーを設定して、アダプターを NDK 対応のミニポートアダプターとして識別します。

    - NDK 機能が有効になっている場合、ミニポートドライバーは**enabled**メンバーを**TRUE**に設定します。それ以外の場合は**FALSE**に設定します。

        > [!NOTE]
        > ミニポートドライバーの NDK 機能の現在の状態を照会して設定する方法の詳細については、「 [Ndk 機能の有効化と無効化](enabling-and-disabling-ndk-functionality.md)」を参照してください。         

    - **Ndkcapabilities**メンバーでは、ミニポートドライバーは、アダプターの機能を指定する[**NDIS\_NDK\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_capabilities)の構造体へのポインターを格納します。

2.  [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出して、アダプターにこれらの属性を設定します。

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 







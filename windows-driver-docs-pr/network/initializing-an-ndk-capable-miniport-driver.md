---
title: NDK 対応ミニポート ドライバーの初期化
description: Network Direct カーネル (NDK) をサポートしているミニポート ドライバーは、その他のミニポート ドライバーと同じ方法で初期化されます。 ただし、追加の NDKPI エントリ ポイントまた登録する必要があります。
ms.assetid: 9C9799AB-75A8-4E9A-8702-D389B73522DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1650f8766e58d6521eb11d46bb613d58364d951b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537595"
---
# <a name="initializing-an-ndk-capable-miniport-driver"></a>NDK 対応ミニポート ドライバーの初期化


Network Direct カーネル (NDK) をサポートしているミニポート ドライバーは、その他のミニポート ドライバーと同じ方法で初期化されます。 ただし、追加の NDKPI エントリ ポイントまた登録する必要があります。

-   [DriverEntry 関数](#driverentry-function)
-   [MiniportSetOptions 関数](#miniportsetoptions-function)
-   [関連トピック](#related-topics)

## <a name="driverentry-function"></a>DriverEntry 関数


すべてのミニポート ドライバーの[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数を初期化します、 [ **NDIS\_ミニポート\_ドライバー\_特性** ](https://msdn.microsoft.com/library/windows/hardware/ff565958)構造体し、それを[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)ように、次のページで説明されています。

-   [ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)
-   [**NDIS ミニポート ドライバーの DriverEntry 関数**](https://msdn.microsoft.com/library/windows/hardware/ff548818)

初期化するときに、NDK 対応のミニポート ドライバーは、次を実行する必要があります、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)構造体。

-   **OidRequestHandler**メンバー、ミニポート ドライバーを登録する必要があります、 [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)をサポートする関数。

    -   すべて[NDKPI Oid](https://msdn.microsoft.com/library/windows/hardware/jj206455)します。

    -   必須の NDIS ミニポート ドライバーは、一般の Oid。

        **注**  これらの必須の Oid の一覧は、次を参照してください。[ミニポート ドライバーに必須の Oid](https://msdn.microsoft.com/library/windows/hardware/ff557139)します。

         

-   **SetOptionsHandler**メンバー、ミニポート ドライバーを登録する必要があります、 [ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)で説明されているとおりに機能[オプションを構成します。ミニポート ドライバー サービス](configuring-optional-miniport-driver-services.md)と次の MiniportSetOptions 関数セクション。

## <a name="miniportsetoptions-function"></a>MiniportSetOptions 関数


NDIS 呼び出し、 [ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数、ミニポート ドライバーの後すぐに[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff548818)関数が返される。 *MiniportSetOptions*ミニポート ドライバーの呼び出しのコンテキストで関数を呼び出す[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)します。

その[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数、NDK 対応のミニポート ドライバーは、次の必要な NDKPI 関数のエントリ ポイント」の説明に従って、NDK 機能とレジスタを登録[省略可能なミニポート ドライバー サービスを構成する](configuring-optional-miniport-driver-services.md):

-   *OpenNDKAdapterHandler* ([*オープン\_NDK\_アダプター\_ハンドラー*](https://msdn.microsoft.com/library/windows/hardware/hh440105))

-   *CloseNDKAdapterHandler* ([*CLOSE\_NDK\_ADAPTER\_HANDLER*](https://msdn.microsoft.com/library/windows/hardware/hh439355))

NDKPI エントリを登録するポイント、これらの関数、ミニポート ドライバーの[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数は、次を実行する必要があります。

1.  初期化を[ **NDIS\_NDK\_プロバイダー\_特性**](https://msdn.microsoft.com/library/windows/hardware/hh451566)構造体。

    **注**  に特に注意してください、**ヘッダー**メンバーの説明。 ミニポート ドライバーでは、NDK 対応のミニポート ドライバーとして自身を識別するために、このメンバーを正しく設定する必要があります。

     

2.  関数のエントリ ポイントを格納、 **OpenNDKAdapterHandler**と**CloseNDKAdapterHandler**構造体のメンバー。

3.  呼び出す、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)で構造体を引数として関数を*OptionalHandlers*パラメーター。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 







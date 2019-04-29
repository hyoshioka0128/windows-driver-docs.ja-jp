---
title: NDK ミニポート アダプターの初期化
description: このセクションは、NDK ミニポート アダプターを初期化する方法を説明します
ms.assetid: 0A920057-3C12-4770-BA08-6C3BB24072EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c05d90fc4c3d713cdea3ce7581ba0807afcdd2c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324974"
---
# <a name="initializing-an-ndk-miniport-adapter"></a>NDK ミニポート アダプターの初期化


Network Direct カーネル (NDK) ミニポート アダプターは、他のミニポート アダプターと同じ方法で初期化されます。NDIS ミニポート アダプターの呼び出す[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)で説明されているとおりに機能[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。 このトピックでは、ミニポート アダプターの NDK に固有の要件を説明します。 *MiniportInitializeEx*関数。

その[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数、ミニポート ドライバーは、次を実行する必要があります。

1.  設定、 [ **NDIS\_ミニポート\_アダプター\_NDK\_属性**](https://msdn.microsoft.com/library/windows/hardware/hh451558)次のように、アダプターの構造体します。

    - ミニポート ドライバーのセット、**ヘッダー** NDK 対応ミニポート アダプターとしてアダプターを識別するためにメンバーをメンバーの説明で説明されているとします。

    - ミニポート ドライバーのセット、**有効**メンバー **TRUE** NDK 機能が有効になっている場合または**FALSE**それ以外の場合。

        > [!NOTE]
        > クエリを実行して、ミニポート ドライバーの NDK 機能の現在の状態の設定の詳細については、次を参照してください。 [NDK 機能の無効化の有効化と](enabling-and-disabling-ndk-functionality.md)します。         

    - **NdkCapabilities**メンバーへのポインターを格納するミニポート ドライバー、 [ **NDIS\_NDK\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451560)構造体を指定します。アダプターの機能です。

2.  呼び出す[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)アダプターのこれらの属性を設定します。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 







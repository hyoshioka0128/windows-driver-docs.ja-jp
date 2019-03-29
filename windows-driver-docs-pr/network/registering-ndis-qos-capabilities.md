---
title: NDIS QoS 機能の登録
description: NDIS QoS 機能の登録
ms.assetid: 03D70079-37A4-4FAA-BF18-ACED3A9E8267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50632ad1dfc185fa50afb961b97a10d672f5fc0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574000"
---
# <a name="registering-ndis-qos-capabilities"></a>NDIS QoS 機能の登録


ネットワーク アダプターの初期化中にミニポート ドライバー regsiter NDIS によるサービス (QoS) の機能の次の品質:

- ネットワーク アダプターをサポートする NDIS QoS ハードウェア機能。

  **注**NDIS 6.30 以降、ミニポート ドライバーは、アダプターが場合にのみをサポートする NDIS QoS ハードウェア機能を登録する必要があります、<strong>\*QOS</strong> INF キーワードの設定がレジストリに存在します。 この場合、ドライバーは、これらの機能を有効になっているやアダプターを無効になっているかどうかに関係なく、NDIS QoS ハードウェアの機能を登録する必要があります。

     

- ネットワーク アダプターで現在有効になっている NDIS QoS ハードウェア機能。

  **注**ミニポート ドライバーの NDIS QoS ハードウェアの機能を有効または無効にできる、  **\*QOS** INF キーワード、レジストリ設定します。 この設定が表示されます、**詳細**ネットワーク アダプターのプロパティ ページ。

     

NDIS QoS INF キーワードの設定の詳細については、次を参照してください。[の NDIS QoS の標準化された INF キーワード](standardized-inf-keywords-for-ndis-qos.md)します。

ミニポート ドライバーを通じて基になるネットワーク アダプターのハードウェアの NDIS QoS 機能の報告、 [ **NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)初期化されている構造体次のように

1.  ミニポート ドライバーを初期化します、**ヘッダー**メンバー。 ドライバーのセット、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_QOS\_機能します。

    NDIS 6.30 以降、ミニポート ドライバーの設定、**リビジョン**のメンバー**ヘッダー** NDIS に\_QOS\_機能\_リビジョン\_1 と**サイズ**NDIS メンバー\_SIZEOF\_QOS\_機能\_リビジョン\_1。

2.  ミニポート ドライバーが、NDIS を設定する場合は、ネットワーク アダプターでは、優先伝送選択アルゴリズム (TSA) をサポートする\_QOS\_機能\_STRICT\_TSA\_でサポートされているフラグ**フラグ**メンバー。 このアルゴリズムの詳細については、次を参照してください。[厳密な優先順位のアルゴリズム](strict-priority-algorithm.md)します。

    **注**  NDIS 6.30 以降、ミニポート ドライバーとネットワーク アダプターの IEEE データ センター ブリッジング (DCB) の NDIS QoS をサポートする必要があります、厳密な優先度をサポート TSA します。

     

3.  ネットワーク アダプターには、メディア アクセス コントロール (MACsec) のセキュリティ処理をバイパスする機能がサポートしている、ミニポート ドライバー設定、NDIS\_QOS\_機能\_MACSEC\_バイパス\_サポートされています。フラグ、**フラグ**メンバー。 MACsec の詳細については、IEEE 802.1AE を参照してください-2006 標準。

    **注**  NDIS 6.30 以降では、ネットワーク アダプターは必要ありません MACsec 処理のバイパスをサポートするためにします。

     

4.  ミニポート ドライバーのセット、 **MaxNumTrafficClasses**メンバーをネットワーク アダプターをサポートする NDIS QoS トラフィック クラスの最大数。 トラフィック クラス定義の送信、または*エグレス*IEEE 802.1p の優先度のレベルと帯域幅の割り当てなど、qos ポリシー。 トラフィック クラスの詳細については、次を参照してください。 [NDIS QoS トラフィック クラス](ndis-qos-traffic-classes.md)します。

    **注**  NDIS 6.30 以降では、ネットワーク アダプターは 3 つのトラフィック クラスの最小値をサポートする必要があります。

     

5.  ミニポート ドライバーのセット、 **MaxNumEtsCapableTrafficClasses** NDIS QoS トラフィック クラス Enhanced Transmission Selection (ETS) アルゴリズムで使用できるネットワーク アダプターの最大数をメンバー。 この値の値未満である必要があります、 **MaxNumTrafficClasses**メンバー。

    ETS の詳細については、次を参照してください。 [Enhanced Transmission Selection (ETS) アルゴリズム](enhanced-transmission-selection--ets--algorithm.md)します。

    **注**  NDIS QoS をサポートするために、ネットワーク アダプターの ETS 対応トラフィック クラスを 2 つの最小値をサポートする必要があります。

     

6.  ミニポート ドライバーのセット、 **MaxNumPfcEnabledTrafficClasses** NDIS QoS トラフィック クラス優先順位に基づくフロー制御 (PFC) アルゴリズムで使用できるネットワーク アダプターの最大数をメンバー。 この値の値未満である必要があります、 **MaxNumTrafficClasses**メンバー。

    PFC の詳細については、次を参照してください。[優先度に基づくフロー制御 (PFC)](priority-based-flow-control--pfc.md)します。

    **注**  NDIS QoS をサポートするために、ネットワーク アダプターの少なくとも 1 つの PFC 対応トラフィック クラスをサポートする必要があります。

     

NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の場合、ドライバーは次の手順に従って、ネットワーク アダプターの NDIS QoS 属性に登録します。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

    ミニポート ドライバーのセット、 **HardwareQOSCapabilities** 、previouslyinitialized へのポインターをメンバー [ **NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)構造体。

    場合のレジストリ設定、  **\*QOS** INF キーワードは、1 つの値を持つ、ネットワーク アダプターの NDIS QoS 機能が有効になっています。 ミニポート ドライバーのセット、 **CurrentQOSCapabilities**同じへのポインターをメンバー [ **NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)構造体。

    場合のレジストリ設定、  **\*QOS** INF キーワードが 0 の値を持つ、ネットワーク アダプターの NDIS QoS 機能が無効になっています。 ミニポート ドライバーを設定する必要があります、 **CurrentQOSCapabilities**メンバーを NULL にします。

2.  ドライバー呼び出し[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)設定と、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

アダプターの初期化プロセスの詳細については、次を参照してください。[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

 

 






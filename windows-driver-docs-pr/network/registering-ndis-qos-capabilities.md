---
title: NDIS QoS 機能の登録
description: NDIS QoS 機能の登録
ms.assetid: 03D70079-37A4-4FAA-BF18-ACED3A9E8267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94c9506554332df2b99cbaad2ce7e24dc5ef41f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842074"
---
# <a name="registering-ndis-qos-capabilities"></a>NDIS QoS 機能の登録


ミニポートドライバーは、ネットワークアダプターの初期化中に、次のサービス品質 (QoS) 機能を NDIS と共に使用します。

- ネットワークアダプターがサポートする NDIS QoS ハードウェア機能。

  **メモ** NDIS 6.30 以降、ミニポートドライバーは、<strong>\*QoS</strong> INF キーワード設定がレジストリに存在する場合にのみ、アダプターがサポートする ndis QoS ハードウェア機能を登録する必要があります。 この場合、ドライバーは、アダプターでこれらの機能が有効になっているか無効になっているかに関係なく、その NDIS QoS ハードウェア機能を登録する必要があります。

     

- ネットワークアダプターで現在有効になっている NDIS QoS ハードウェア機能。

  **メモ** ミニポートドライバーの NDIS QoS ハードウェア機能は、レジストリの **\*QoS** INF キーワード設定を使用して有効または無効にすることができます。 この設定は、ネットワークアダプターの **[詳細**設定] プロパティページに表示されます。

     

NDIS QoS INF キーワード設定の詳細については、「 [Ndis qos の標準化](standardized-inf-keywords-for-ndis-qos.md)された inf キーワード」を参照してください。

ミニポートドライバーは、次の方法で初期化される[**NDIS\_qos\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)の構造を通じて、基になるネットワークアダプターのハードウェア NDIS qos 機能を報告します。

1.  ミニポートドライバーは、**ヘッダー**メンバーを初期化します。 ドライバーは、**ヘッダー**の**TYPE**メンバーを NDIS\_OBJECT\_TYPE\_QOS\_機能に設定します。

    NDIS 6.30 以降では、ミニポートドライバーは、**ヘッダー**の**リビジョン**メンバーを NDIS\_QOS\_機能\_リビジョン\_1、 **SIZE**メンバーを NDIS\_SIZEOF\_qos\_機能\_リビジョン\_1 に設定します。

2.  ネットワークアダプターが厳密な優先順位の伝送選択アルゴリズム (TSA) をサポートしている場合、ミニポートドライバーは、**フラグ**メンバーで TSA\_supported フラグを厳格\_に\_、NDIS\_QOS の\_機能を設定します。 このアルゴリズムの詳細については、「 [Strict Priority algorithm](strict-priority-algorithm.md)」を参照してください。

    **注**  Ndis 6.30 以降では、IEEE データセンターブリッジング (DCB) の ndis QoS をサポートするミニポートドライバーおよびネットワークアダプターが、厳密な優先順位の TSA をサポートしている必要があります。

     

3.  ネットワークアダプターが media access control security (MACsec) の処理をバイパスする機能をサポートしている場合、ミニポートドライバーは、**フラグ**メンバーでサポートされているフラグを\_バイパス\_\_MACSEC に NDIS\_QOS\_機能を設定します。 MACsec の詳細については、「IEEE 802.1 AE-2006 標準」を参照してください。

    **注**  NDIS 6.30 以降では、ネットワークアダプターは macsec 処理のバイパスをサポートする必要はありません。

     

4.  ミニポートドライバーは、ネットワークアダプターがサポートする NDIS QoS トラフィッククラスの最大数に**MaxNumTrafficClasses**メンバーを設定します。 Traffic クラスは、IEEE 802.1 p の優先度レベルや帯域幅の割り当てなど、QoS の*送信または*送信のポリシーを定義します。 トラフィッククラスの詳細については、「 [NDIS QoS Traffic classes](ndis-qos-traffic-classes.md)」を参照してください。

    **注**  NDIS 6.30 以降では、ネットワークアダプターは3つ以上のトラフィッククラスをサポートする必要があります。

     

5.  ミニポートドライバーは、 **MaxNumEtsCapableTrafficClasses**メンバーを、network Adapter が Enhanced 伝送選択 (送信) アルゴリズムで使用できる NDIS QoS トラフィッククラスの最大数に設定します。 この値は、 **MaxNumTrafficClasses**メンバーの値以下である必要があります。

    設定の詳細については、「 [Enhanced 伝送選択 (送信) アルゴリズム](enhanced-transmission-selection--ets--algorithm.md)」を参照してください。

    ネットワークアダプターが NDIS QoS をサポートするには、少なくとも2つのトラフィッククラスがサポートされている必要があります **。  **

     

6.  ミニポートドライバーは、 **MaxNumPfcEnabledTrafficClasses**メンバーを、優先順位ベースのフロー制御 (pfc) アルゴリズムでネットワークアダプターが使用できる NDIS QoS トラフィッククラスの最大数に設定します。 この値は、 **MaxNumTrafficClasses**メンバーの値以下である必要があります。

    PFC の詳細については、「[優先順位ベースのフロー制御 (pfc)](priority-based-flow-control--pfc.md)」を参照してください。

    ネットワークアダプターが NDIS QoS をサポートするには、少なくとも1つの PFC 対応の traffic クラスをサポートしている必要が**あり  。**

     

NDIS がミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ドライバーは次の手順に従って、ネットワークアダプターの NDIS QoS 属性を登録します。

1.  ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の構造を初期化します。

    ミニポートドライバーは、 **HardwareQOSCapabilities**メンバーを、前に初期化された[**NDIS\_QOS\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)の構造へのポインターに設定します。

    **\*QOS** INF キーワードのレジストリ設定の値が1の場合、NDIS QOS 機能はネットワークアダプターで有効になります。 ミニポートドライバーは、 **CurrentQOSCapabilities**メンバーを、同じ[**NDIS\_QOS\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)の構造へのポインターに設定します。

    **\*QOS** INF キーワードのレジストリ設定の値が0の場合、NDIS QOS 機能はネットワークアダプターで無効になっています。 ミニポートドライバーでは、 **CurrentQOSCapabilities**メンバーを NULL に設定する必要があります。

2.  ドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出し、 *miniportattributes*パラメーターを[**NDIS\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)へのポインターに設定します。\_ハードウェア\_\_属性の構造をサポートします。

アダプター初期化プロセスの詳細については、「[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

 

 






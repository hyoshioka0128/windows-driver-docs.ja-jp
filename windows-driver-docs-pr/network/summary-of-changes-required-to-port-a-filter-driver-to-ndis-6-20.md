---
title: フィルター ドライバーを NDIS 6.20 に移植するために必要な変更の概要
description: フィルター ドライバーを NDIS 6.20 に移植するために必要な変更の概要
ms.assetid: faf83399-b9ac-41b3-a891-0142ded422b3
keywords:
- NDIS 6.20 WDK、移植フィルタードライバー
- NDIS 6.20 WDK へのフィルタードライバーの移植
- ドライバーのフィルター (WDK)
- ドライバーのフィルターを適用し、NDIS 6.20 に移植する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9b5bea66179d54a7037059660b79141877b5dbe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841812"
---
# <a name="summary-of-changes-required-to-port-a-filter-driver-to-ndis-620"></a>フィルター ドライバーを NDIS 6.20 に移植するために必要な変更の概要





このトピックでは、NDIS 6 を移植するために必要な変更について説明します。*x*フィルタードライバーを NDIS 6.20 に適用します。

NDIS 6.20 では、以前のバージョンの NDIS との下位互換性が維持されます。 旧バージョンとの互換性の詳細については、「 [NDIS 6.20 の旧バージョン](ndis-6-20-backward-compatibility.md)との互換性」を参照してください。

NDIS 6.20 環境をサポートするようにフィルタードライバーを更新するには、次のように NDIS 6.x フィルタードライバーを変更する必要があります。

<a href="" id="build-environment"></a>**ビルド環境**  
プリプロセッサ定義 NDIS61 または NDIS60 を NDIS620 に置き換えます。

<a href="" id="general-porting-requirements"></a>**一般的な移植の要件**  
-   旧式のインターフェイスを NDIS 6.20 バージョンに置き換えます。 互換性のために残されているインターフェイスの詳細については、「 [NDIS 6.20 の古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)」を参照してください。

-   64を超えるプロセッサをサポートするように、次のインターフェイスを更新します。

    -   受信側 scaling (RSS)
    -   プロセッサ情報デバイスドライバーインターフェイス
    -   リソース割り当て
    -   読み取りと書き込みのロック

    64を超えるプロセッサをサポートする方法の詳細については、「 [NDIS 6.20 で64を超えるプロセッサをサポートする](support-for-more-than-64-processors-in-ndis-6-20.md)」を参照してください。

<a href="" id="driver-initialization"></a>**ドライバーの初期化**  
-   [**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)に渡される[**ndis\_フィルター\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)の構造の**MajorNdisVersion**および**MinorNdisVersion**メンバーで、ndis のバージョンを6.20 に設定します。プロシージャ.

-   NDIS\_フィルター\_ドライバー\_特性の構造にあるフィルタードライバー**のバージョンを**、適切なドライバー固有の値に**設定します**。

<a href="" id="filter-module-attach-and-detach-operations"></a>**フィルターモジュールのアタッチとデタッチの操作**  
-   最新バージョンのミニポートアダプター機能の提供情報インターフェイスを使用します。 次のインターフェイスの機能が更新されました。
    -   電源管理
    -   Receive side scaling (RSS)
    -   ハードウェアアシスト (VMQ)
-   次の構造の更新されたバージョンを使用します。

    -   [**NDIS\_フィルター\_\_パラメーターをアタッチする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)
    -   [**NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

    NDIS 構造のバージョン情報については、「 [Ndis バージョン情報の指定](specifying-ndis-version-information.md)」を参照してください。

<a href="" id="send-and-receive-data-paths"></a>**データパスの送受信**  
-   更新されたバージョンの[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体を使用します。

-   必要に応じて、バーチャルマシンキュー (VMQ) インターフェイスをサポートします。 VMQ の詳細については、「[仮想マシンキュー (vmq) (NDIS 6.20)](virtual-machine-queue--vmq--in-ndis-6-20.md)」を参照してください。

 

 






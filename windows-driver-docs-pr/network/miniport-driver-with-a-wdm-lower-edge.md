---
title: WDM の下端を含むミニポート ドライバー
description: WDM の下端を含むミニポート ドライバー
ms.assetid: e3acbcfe-b63d-441d-ab5f-26ee54a5d3ec
keywords:
- NDIS-WDM ミニポートドライバー WDK ネットワーク、NDIS-WDM ミニポートドライバーについて
- NDIS-WDM ミニポートドライバー WDK ネットワーク、コンポーネント
- NDIS ミニポートドライバー WDK ネットワークの下端
- WDM 低エッジの WDK ネットワーク
- NDIS ミニポートドライバー WDK ネットワーク、WDM の下限
- WDM 低速の WDK ネットワーク、WDM のダウンエッジの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 356f2c2d33c0073f6a7c031d5ac026a598039e1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844235"
---
# <a name="miniport-driver-with-a-wdm-lower-edge"></a>WDM の下端を含むミニポート ドライバー





Wdm の下部にあるミニポートドライバー (NDIS-WDM ミニポートドライバー) は、wdm のヘッダーファイルをドライバーのソースファイルに含める必要があることを指定する WDM 規則に従います。 NDIS-WDM ミニポートドライバーを必要とする場合は、WDM ヘッダーファイルを介してカーネルモードルーチンを呼び出す必要があります。 通常、NDIS ミニポートドライバーは、NDIS が提供する関数を呼び出すだけで済みます。 この制限は、ndis[ドライバー](ndis-drivers.md)セクションの図で ndis ミニポートドライバーを ndis でラップする方法によって示されています。 一般的な NDIS ミニポートドライバーは WDM ドライバーと呼ばれませんが、NDIS 自体は wdm 規則に従います。これは、NDIS 自体が WDM 規則に従っているためです。

次の図は、WDM の下エッジを使用して USB ドライバースタックとインターフェイスを持つ NDIS-WDM ミニポートドライバーを示しています。

![wdm の下側のエッジを使用して usb ドライバースタックとやり取りする ndis-wdm ミニポートドライバーを示す図](images/nonndslo.png)

次の一覧では、前の図に示されているコンポーネントについて説明します。

<a href="" id="ipx-spx-compatible-and-tcp-ip"></a>IPX/SPX 互換と TCP/IP  
基になるミニポートドライバーを使用してパケットを送信する[NDIS プロトコルドライバー](ndis-protocol-drivers.md) 。

<a href="" id="ndis"></a>NDIS  
階層化されたネットワークドライバー間の標準インターフェイスを提供する Ndis ドライバー。

<a href="" id="ndis-wdm-miniport-driver-for-usb"></a>USB 用 NDIS-WDM ミニポートドライバー  
USB ドライバースタックとのインターフェイスを持つ NDIS WDM ミニポートドライバー。

<a href="" id="usb-client-drivers"></a>USB クライアントドライバー  
ベンダーが提供するその他の USB クライアントドライバー。

<a href="" id="usb-class-interface"></a>USB クラスインターフェイス  
Usb クライアントドライバーが usb ドライバースタックとのインターフェイスに使用できる[Usb ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85))と[i/o 要求](https://docs.microsoft.com/previous-versions/ff537421(v=vs.85))。

<a href="" id="usb-driver-stack"></a>USB ドライバースタック  
USB デバイスのドライバースタック。 詳細については、「 [USB ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 






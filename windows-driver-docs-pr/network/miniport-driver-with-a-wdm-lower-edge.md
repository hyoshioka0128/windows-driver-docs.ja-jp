---
title: WDM の下端を含むミニポート ドライバー
description: WDM の下端を含むミニポート ドライバー
ms.assetid: e3acbcfe-b63d-441d-ab5f-26ee54a5d3ec
keywords:
- NDIS WDM ミニポート ドライバー WDK ネットワー キング、NDIS WDM ミニポート ドライバーについて
- NDIS WDM ミニポート ドライバー WDK ネットワー キング、コンポーネント
- 下端の NDIS ミニポート ドライバー WDK ネットワーク
- WDM 低い edge WDK ネットワーク
- 下端の NDIS ミニポート ドライバー WDK ネットワー キング、WDM 下端について
- WDM 低い edge WDK ネットワー キング、WDM 下端について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f7b8a16287d9333b8fed8428072cd6a207482cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380908"
---
# <a name="miniport-driver-with-a-wdm-lower-edge"></a>WDM の下端を含むミニポート ドライバー





WDM 低い edge (NDIS WDM ミニポート ドライバー) のミニポート ドライバーでは、ドライバーのソース ファイルで WDM ヘッダー ファイルを含める必要があることを指定する WDM ルールに従います。 NDIS WDM のミニポート ドライバーには、その下端にカーネル モードのルーチンを呼び出す WDM ヘッダー ファイルが必要です。 通常、NDIS ミニポート ドライバーは、NDIS を提供する関数を呼び出すだけする必要があります。 この制限は NDIS の折り返しの図の NDIS ミニポート ドライバーで表示されます、 [NDIS ドライバー](ndis-drivers.md)セクション。 通常の NDIS ミニポート ドライバーは WDM ドライバーが呼び出されませんが、直接規則に従っていない WDM 自体 NDIS WDM 規則に従っているため。

次の図は、WDM 下端を使用して、USB ドライバー スタックとやり取りする NDIS WDM ミニポート ドライバーを示します。

![wdm 下端を使用して、usb ドライバー スタックとやり取りする ndis wdm ミニポート ドライバーを示す図](images/nonndslo.png)

次の一覧には、前の図に示すコンポーネントについて説明します。

<a href="" id="ipx-spx-compatible-and-tcp-ip"></a>IPX/SPX 互換性のあるおよび TCP/IP  
[NDIS ドライバーのプロトコル](ndis-protocol-drivers.md)基になるミニポート ドライバーを使用してパケットを送信します。

<a href="" id="ndis"></a>NDIS  
多層型ネットワークのドライバーの間の標準的なインターフェイスを提供する Ndis.sys ドライバー。

<a href="" id="ndis-wdm-miniport-driver-for-usb"></a>USB の NDIS WDM ミニポート ドライバー  
NDIS WDM ミニポート ドライバーの USB ドライバー スタックとのインターフェイスします。

<a href="" id="usb-client-drivers"></a>USB クライアント ドライバー  
その他のベンダーから提供された USB クライアント ドライバー。

<a href="" id="usb-class-interface"></a>USB クラス インターフェイス  
[USB ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85))と[I/O 要求](https://docs.microsoft.com/previous-versions/ff537421(v=vs.85))USB クライアント ドライバーが使用できることを USB ドライバー スタックとのインターフェイス。

<a href="" id="usb-driver-stack"></a>USB ドライバー スタック  
USB デバイスのドライバー スタックです。 詳細については、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 






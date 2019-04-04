---
title: WDM 下端のミニポート ドライバーの初期化
description: WDM 下端のミニポート ドライバーの初期化
ms.assetid: 1c5b0ec0-5d63-423d-af21-ffd8990f6160
keywords:
- NDIS WDM ミニポート ドライバー WDK ネットワーク、初期化しています
- NDIS WDM ミニポート ドライバー WDK、ネットワーク上の端
- ミニポート ドライバー WDK ネットワーク、初期化しています
- NDIS ミニポート ドライバー WDK、初期化しています
- 逆シリアル化された NDIS ミニポート ドライバー WDK ネットワーク
- 下端の NDIS ミニポート ドライバー WDK ネットワー キング、ドライバーの初期化
- WDM 低い edge WDK ネットワー キング、ドライバーの初期化
- ミニポート ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1db5a94c97047f82ac2a1f48b8f64f0b1a6a023
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556953"
---
# <a name="initializing-a-miniport-driver-with-a-wdm-lower-edge"></a>WDM 下端のミニポート ドライバーの初期化





NDIS ミニポート ドライバーを呼び出すミニポート ドライバーがオペレーティング システムによって読み込まれた後[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)ミニポート ドライバーを管理するミニポート インスタンスを初期化します。 WDM 下端のあるミニポート インスタンス経由で通信、ミニポート ドライバーはその通信を設定する特定の情報を取得する必要があります。

このミニポート インスタンスの初期化中に、ミニポート ドライバーを呼び出す必要があります、 [ **NdisMGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff563592)との通信を設定するために必要なデバイス オブジェクトを取得する関数をWDM インターフェイスを通じてミニポート インスタンス。 この呼び出しで、ミニポート ドライバーがでミニポート インスタンスに、ハンドルを渡します、 *MiniportAdapterHandle*パラメーターおよびへのポインターを受け取るバッファー [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)構造体。 ミニポート ドライバーが次のデバイス オブジェクトを取得したポインターを使用して ( *NextDeviceObject*パラメーター) を作成し、Irp を送信します。 詳細については、[Irp の処理](https://msdn.microsoft.com/library/windows/hardware/ff546847)を参照してください。

WDM 下端のミニポート ドライバーは、逆シリアル化されたミニポート ドライバーである必要があります。 逆シリアル化されたミニポート ドライバーが、独自の送信キューを管理し、すぐにこれらの要求を処理するためにリソース不足があるときに、内部的に要求を受信ミニポート ドライバーが逆シリアル化しない場合、NDIS は、このキューを管理します。 NDIS WDM のミニポート ドライバーは、NDIS 呼び出しのコンテキスト外でパケットを送受信しているために、逆シリアル化する必要があります。 ミニポート インスタンスの初期化中に、NDIS WDM ミニポート ドライバーは、逆シリアル化された機能を指定する必要があります。 すべての NDIS 6.0 とそれ以降のミニポート ドライバーが逆シリアル化します。

NDIS WDM のミニポート ドライバーは中間ドライバー (ドライバーのミニポート ドライバーのインターフェイスを上部と下部にあるプロトコル ドライバー インターフェイスを公開します) であることに注意してください。

 

 






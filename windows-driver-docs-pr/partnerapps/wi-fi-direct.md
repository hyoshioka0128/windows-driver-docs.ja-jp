---
title: Wi-Fi Direct
description: Wi-Fi Direct
ms.assetid: 52D09B1D-5832-48C9-B200-46B8DDC14BE5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a5c1f5a1bca8bde86b33a8b1089d9d34afe21f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538761"
---
# <a name="wi-fi-direct"></a>Wi-Fi Direct


Windows 10 と関連付けられている Wi-Fi Direct Api WDI ドライバーでは、NDIS ドライバーおよび Windows 8.1 で関連する SoftAP Api を置き換えます。 Windows 10 で NDIS ドライバーで動作する SoftAP API を使用して継続できますが、Windows 8.1 以降の API は非推奨します。 IDot11AdHocManager と関連するインターフェイスが含まれています。

Windows 10 のすべての機能をする必要があります、Wi-Fi Direct WinRT Api WDI ドライバーの代わりに使用します。

Wi-Fi Direct WinRT Api の一部を使用して、クラシック Windows アプリケーションでは、ただし。 たとえばクラシック Windows アプリケーションで WFDOpenHandle の代わりに Wi-Fi Direct WinRT Api と関連 Api を使用することができます。 WiFiDirectLegacySettings クラスは、それをサポートしているデバイスに接続して、Wi-Fi Direct デバイスによって提供されるサービスを使用する Wi-Fi Direct をサポートしないデバイスを使用できます。

WiFiDirectLegacySettings は、SSID とパスワードを指定することができます。 クラシック Windows アプリケーションで WiFiDirectLegacySettings を使用する方法の例は、次を参照してください。、 [WiFiDirectLegacyAPDemo\_v1.0.zip](https://go.microsoft.com/fwlink/?LinkId=617905) Microsoft ダウンロード センターからダウンロードします。

モバイル ホット スポットは、Windows 10 バージョン 1607 以降はサポートされています。 モバイル ホット スポットは、モバイル ブロード バンド ケーブルの機能の強化されたバージョンです。 モバイル ホット スポットと Wi-Fi Direct グループ所有者のレガシ機能を同時に使用できないことに注意してください。 さらに、モバイル ホット スポットは、Wi-Fi Direct のすべてのシナリオに優先します。

デスクトップ アプリケーションの開発者は、このサンプルを使用して、非推奨の WlanHostedNetwork を置換する方法について\*新しい WinRT API でのユニバーサル Windows アプリケーションにアプリケーションを変更することがなく API。 これらの API には、アプリケーションが、Wi-Fi Direct グループ所有者 (移動) へのアクセス ポイント (AP) として機能する開始できるようにします。 これにより、このアプリケーションを実行している Windows デバイスに接続する Wi-Fi Direct をサポートしないようにし TCP または UDP 経由で通信するデバイスです。 API を使用すると、必要に応じて、SSID とパスフレーズを指定する開発者または使用してランダムに生成されたものです。

**注**  でクラシック Windows アプリ、Package.appxmanifest ファイルがないため、WinRT デバイス機能を設定する必要はありません。

 

## <a name="resources"></a>参考資料


### <a name="recorded-sessions"></a>セッションの録画

-   [Wi-Fi Direct と Wi-Fi Direct Services API (サンプル コードを含む)](https://go.microsoft.com/fwlink/?LinkId=617632)

### <a name="articles"></a>記事

-   [Wi-Fi Direct サービス API](https://go.microsoft.com/fwlink/?LinkId=617633)
-   [ドライバーの開発で新機能]( https://go.microsoft.com/fwlink/?LinkId=617634)
-   [Win32 アプリでは、WinRT API を使用します。]( https://go.microsoft.com/fwlink/?LinkId=617635)

### <a name="wi-fi-direct-in-windows-8"></a>Wi-Fi Direct では、Windows 8

-   [Windows 8 で、Wi-Fi Direct を理解します。](https://go.microsoft.com/fwlink/?LinkId=617636)
-   [エキスパート パネル。接続されているアプリ](https://go.microsoft.com/fwlink/?LinkId=617637)
-   [Wi-Fi Direct を使用している Windows アプリをビルドする (Windows 8.1)](https://go.microsoft.com/fwlink/?LinkId=617638)

 

 






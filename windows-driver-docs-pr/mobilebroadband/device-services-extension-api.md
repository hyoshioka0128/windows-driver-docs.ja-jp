---
title: デバイス サービス拡張 API
description: デバイス サービス拡張 API
ms.assetid: e1539ae1-78fd-4d79-81bf-4030e69e191c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d31db3adff55b008392fcbf834a115b33026129
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380268"
---
# <a name="device-services-extension-api"></a>デバイス サービス拡張 API


Windows 対応のモバイル ブロード バンド デバイスは、デバイスのサービスとしてサポートされている各機能をプロジェクトします。 サービスには IP 接続 (接続およびモバイル ブロード バンド ネットワークから切断する機能)、電話帳、SIM Toolkit、SMS、USSD などがあります。 各デバイスのサービスでは、対応する GUID があります。 すべてのコントロールのメッセージとモバイル ブロード バンドの一般的なドライバーとデバイスの実行要求に関連付けられているサービスを識別する GUID の間で交換される非 IP パケット。 コマンド識別子 (Cid) と状態を示す値のコードは、サービスの GUID の名前空間で定義されます。 たとえば、電話帳 and SIM Toolkit が両方同じコードを共有 CID が、デバイス サービス要求で交換される GUID によって識別されます。

Windows のワイヤレス プラットフォームでネイティブに実装されていないすべてのデバイス サービスは、デバイス サービス拡張機能 API でアクセスできます。 この API では、デバイスの機能にアクセスする、独立系ハードウェア ベンダー (IHV) のソフトウェアを直接パイプを提供します。 このパイプは、次の図に示すように、WWAN サービス、デバイスにモバイル ブロード バンドの一般的なドライバーからのコンジットを提供します。

![デバイス サービス](images/mb-fig1-deviceservices.png)

Windows のワイヤレス プラットフォームでは、次のアプリ機能の Api をサポートしています。

-   デバイスのサービスを列挙します。

-   デバイス サービスを開く/閉じる.

-   特定のデバイス サービスに管理コマンドを送信します。

-   データを送信する (またはからのデータが表示される) 特定のデバイス サービス

-   特定のデバイス サービスからイベントを「迷惑な」デバイスの登録します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一覧](list-of-mobile-broadband-windows-runtime-apis.md)

 

 







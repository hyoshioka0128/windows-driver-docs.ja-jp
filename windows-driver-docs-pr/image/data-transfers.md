---
title: データ転送
description: データ転送
ms.assetid: 55ef8125-40d3-44f3-8520-cc3a0912c3d2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccead64857af5882fbe605e3c6c5d210aa25a6df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530973"
---
# <a name="data-transfers"></a>データ転送





WIA ミニドライバーの主な目的は、デバイスからアプリケーションにデータを転送します。 カメラが、データが以前にキャプチャした画像、オーディオ、またはビデオ クリップで可能性があります。 スキャナーでデバイスは、スキャナーから取得するようにデータを転送する必要があります。

オペレーティング システムで Windows Vista、WIA がある 2 つの方法で、アプリケーションに、デバイスからデータを転送する前に両方に基づいて[TYMED](understanding-tymed.md)します。 最初は、デバイスが、WIA サービスにイメージ データのバンドを取得するメモリ内転送をでした。 2 番目の方法では、WIA サービスへのファイル転送をしました。 WIA サービスは、データを受信して、要求元のアプリケーションに転送したことに注意してください。

Windows vista では、新しい種類の転送を提供されています。**IStream**-ベースの転送。 この転送モデルは 2 つのインターフェイスに依存 (**IWiaItem2**と**IWiaDevMgr2**) は Windows Vista の新機能です。 (これら両方のインターフェイスについては、Microsoft Windows SDK のドキュメント。)Windows Vista と従来のドライバーとアプリケーション間で操作できるようにする互換性レイヤーがあります。 この互換レイヤーがいくつかの制限が記載されている、 [IStream 転送との互換性を実現する](achieving-compatibility-with-istream-transfers.md)セクション。

このセクションには、次のトピックが含まれています。

[メモリ内転送](in-memory-transfers.md)

[ファイル転送](file-transfers.md)

[IStream データ転送](istream-data-transfers.md)

データ転送の詳細については、[WIA アプリケーションにデータを転送する](transferring-data-to-a-wia-application.md)を参照してください。

 

 





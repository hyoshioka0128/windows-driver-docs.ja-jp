---
title: WIA 互換性レイヤーのデータ転送の概要
description: WIA 互換性レイヤーのデータ転送の概要
ms.assetid: 4c88474e-f776-4876-a15f-c9d6fb0d20e5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14df38f512094aad337741984f3d3cf093b3023f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360617"
---
# <a name="wia-compatibility-layer-data-transfers-overview"></a>WIA 互換性レイヤーのデータ転送の概要


転送の互換性レイヤーなし、Windows Vista WIA ドライバーがありましたレガシー システムと Windows Vista のアプリケーションからのデータ転送を実行するには TYMED およびストリーム ベースのデータ転送のスタイルの両方を実装します。 同様に、Windows Vista の WIA アプリケーションがレガシ エンジンと Windows Vista のドライバーからのデータ転送を実行するには、(異なるコールバックの実装) による転送の両方のスタイルを実装するためにありました。 WIA 互換性レイヤーとドライバーの種類は、WIA アプリケーションに対して透過的と Windows Vista WIA ドライバーが任意の転送がレガシ コードと対処する必要はありません。

転送ケースを 2 つの互換性レイヤが必要なそれぞれのさらに分割して 2 つのサブ カテゴリがあります。

1.  レガシ アプリケーションは、Windows Vista ドライバーからデータを転送する:
    1.  ファイル転送:アプリケーション呼び出し**IWiaDataTransfer::idtGetBandedData**します。
    2.  コールバック転送:アプリケーション呼び出し**IWiaDataTransfer::idtGetData**します。

2.  従来、ドライバーからデータを転送する Windows Vista アプリケーション:
    1.  ファイル転送:互換レイヤーは、従来のドライバーを使用したファイル転送を開始します。
    2.  コールバック転送:互換レイヤーは、従来のドライバーを使用したコールバックの転送を開始します。

WIA ドライバーが Windows Vista ドライバーまたはレガシ ドライバーがあるか判断にレイヤーが互換性を使用するかどうかを判断する最初の手順。 WIA サービスはからドライバーを返すバージョン番号を調べることでこれを判断[ **IStiUSD::GetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543817)します。 従来、ドライバー返します STI\_バージョンのバージョン番号、Windows Vista ドライバーが STI を返す必要がありますが、\_バージョン\_3。 このバージョン番号は、Windows Vista プロパティで、WIA WIA COM プロキシ (および WIA アプリケーション) に公開されます\_DIP\_STI\_ドライバー\_バージョン。

アプリケーションが Windows Vista の WIA アプリケーションまたは従来の WIA アプリケーションは簡単かを判断する互換性レイヤーを使用するかどうかを決定するは、次の手順は、: アプリケーションから呼び出す場合**IWiaDataTransfer::idtGetBandedData**または**IWiaDataTransfer::idtGetData** 、アプリケーションから呼び出す場合は、従来の WIA アプリケーションを**IWiaTransfer::Download** Windows Vista の WIA アプリケーションです。

ストリーム ベースのデータ転送の新しいモデルと、WIA サービスは不要になった区別 TYMED\_コールバックと TYMED\_ファイル (または TYMED\_マルチページ\_コールバックと TYMED\_マルチページ\_ファイルの場合)。 代わりにはだけ TYMED\_ファイルと TYMED\_マルチページ\_ファイル。 TYMED\_マルチページ\_複数ページの TIFF (または PDF) のスキャンをサポートするドライバーを許可するファイルが必要です。 詳細については、TYMED で定数を参照してください[理解 TYMED](understanding-tymed.md)します。

WIA がメモリ ビットマップ形式をサポートしていません**WiaImgFmt\_MEMORYBMP** Windows Vista のドライバーでします。

Windows Vista のドライバーでは、転送中にイメージ全体をキャッシュ、ドライバーではなく、バンド内のデータを転送する更新プログラムのメッセージを送信できます。 この形式の転送は、すぐに、スクロール フィード スキャナーによるスキャンなど、転送されるイメージのサイズを決定することはできませんのスキャン中にデータを転送する場合に便利です。 バンドに画像データを転送するために、ドライバーを呼び出す必要があります**IStream::Seek**内で渡されたストリームに[ **IWiaTransferCallback::GetNextStream**](https://msdn.microsoft.com/library/windows/hardware/ff545039)します。

TYMED と転送のストリーム ベースの詳細については、次を参照してください。 [Data Transfers](data-transfers.md)します。

**IWiaDataTransfer**、 **IWiaTransfer**、および**IStream**インターフェイスについては、Microsoft Windows SDK ドキュメントで説明します。

 

 





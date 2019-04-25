---
title: ネットワーク アダプターの WDF クラス拡張機能 (NetAdapterCx)
description: ネットワーク アダプターの WDF クラス拡張機能 (NetAdapterCx)
ms.assetid: 74719A80-AE66-410F-85B7-31B6F455A818
keywords:
- ネットワーク アダプターのクラス拡張機能、ネットワーク アダプターの WDF クラス拡張機能、NetAdapterCx、NetCx
ms.date: 03/21/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.custom: 19H1
ms.openlocfilehash: 41184d69be8382429ae6b59e8606afb49c729c0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375391"
---
# <a name="network-adapter-wdf-class-extension-netadaptercx"></a>ネットワーク アダプターの WDF クラス拡張機能 (NetAdapterCx)

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

## <a name="overview"></a>概要

Windows 10 バージョン 1703 以降の Windows Driver Kit (WDK) には、ネットワーク インターフェイス コントローラー (NIC) 用の KMDF ベースのクライアント ドライバーを作成できるネットワーク アダプターの WDF クラス拡張機能モジュール (NetAdapterCx) が含まれています。 NetAdapterCx によって、WDF の機能と柔軟性、NDIS のネットワーク パフォーマンスを利用し、NIC 用のドライバーを簡単に作成できます。

以前のバージョンの Windows では、WDF と NDIS にはそれぞれ利点がありましたが、相互運用性は良くありませんでした。 NIC ドライバーを作成するには、NDIS ミニポート ドライバーを作成する必要がありました。 NDIS ミニポート ドライバーで WDF を使用するには、ドライバーに追加のコードを記述する必要がありましたが、それでもアクセスできるのは WDF 機能のごく一部のみでした。

対照的に、NetAdapterCx モデルでは、NIC 用の実際の WDF ドライバーを作成します。 つまり、NetAdapterCx ドライバーは WDF の全機能だけでなく、NetAdapter クラス拡張機能のネットワーク固有の API と I/O サポートにもアクセスできます。 以下のブロック図に示すように、NetAdapterCx は NDIS の背後で動作していますが、開発者に代わって NDIS とのすべての対話を処理しています。

<img src="images/architecture.png" alt="NetAdapterCx architecture" title="NetAdapterCx のアーキテクチャ" width="600"/>

## <a name="additional-info"></a>追加情報

NetAdapterCx を使用する利点を説明したビデオについては、「[Network Adapter Class Extension:Overview (ネットワーク アダプター クラス拡張機能: 概要)](https://aka.ms/netadapter/video1)」(Channel 9) をご覧ください。

NDIS 6.x ミニポート ドライバーを NetAdapterCx NIC ドライバー モデルに移植する方法については、「[Porting NDIS miniport drivers to NetAdapterCx (NDIS ミニポート ドライバーの NetAdapterCx への移植)](porting-ndis-miniport-drivers-to-netadaptercx.md)」を参照してください。

GitHub 上のドライバー サンプルをすぐに利用するには、[NetAdapter-Cx-Driver-Samples](https://github.com/Microsoft/NetAdapter-Cx-Driver-Samples) リポジトリを複製してください。

NetAdapterCx 自体のソース コードを確認する場合、またはステップ実行のデバッグを実行する場合は、GitHub 上の [Network-Adapter-Class-Extension](https://github.com/Microsoft/Network-Adapter-Class-Extension) リポジトリを参照してください。

NetAdapterCx クライアント ドライバーを開発するときに Microsoft と連携する場合、またはクラス拡張機能についてフィードバックがある場合は、[電子メール](mailto:netadapter@microsoft.com)を送信してください。

今後のロードマップとコラボレーションの機会について説明したビデオについては、「[Network Adapter Class Extension:Roadmap and Collaboration (ネットワーク アダプター クラス拡張機能: ロードマップとコラボレーション)](https://aka.ms/netadapter/video4)」(Channel 9) をご覧ください。

## <a name="topics"></a>トピック

このセクションでは、次のトピックについて説明します。

* [NDIS ミニポート ドライバーの NetAdapterCx への移植](porting-ndis-miniport-drivers-to-netadaptercx.md)
* [NetAdapterCx クライアント ドライバーの構築](building-a-netadaptercx-client-driver.md)
* [NetAdapterCx クライアント ドライバーの INF ファイル](inf-files-for-netadaptercx-client-drivers.md)
* [NetAdapterCx でのオブジェクトの有効期間の管理](managing-the-lifetime-of-objects-in-netadaptercx.md)
* [構成情報へのアクセス](accessing-configuration-information.md)
* [制御要求の処理](handling-control-requests.md)
* [NetAdapterCx クライアント ドライバーのデバッグ](debugging-a-netadaptercx-client-driver.md)
* [ネットワーク データの転送](transferring-network-data.md)
* [NetAdapterCx Receive Side Scaling (RSS)](netadaptercx-receive-side-scaling-rss-.md)
* [電源管理の構成](configuring-power-management.md)
* [NDIS-WDF 関数に対応する関数](ndis-wdf-function-equivalents.md)
* [NetAdapterCx の制限事項](netadaptercx-limitations.md)
* [モバイル ブロードバンド (MBB) WDF クラス拡張機能 (MBBCx)](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)

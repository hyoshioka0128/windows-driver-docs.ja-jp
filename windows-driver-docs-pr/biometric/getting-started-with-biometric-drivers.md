---
title: 生体認証ドライバーの概要
description: 生体認証ドライバーの概要
ms.assetid: 7f5dcac2-db0d-4ddd-9e57-886db324e38b
keywords:
- 生体認証ドライバー WDK、生体認証ドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15baea7067fd0e062f538b2611d899657e168ac3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364711"
---
# <a name="getting-started-with-biometric-drivers"></a>生体認証ドライバーの概要


Windows 生体認証フレームワーク (WBF) は、Windows 7 および以降のバージョンの Windows で生体認証汎用的なアーキテクチャです。

WBF には、Windows 生体認証ドライバー インターフェイス (WBDI) と呼ばれる IOCTL ベースのドライバー インターフェイスにはおよび Windows 生体認証サービス (WBS) と呼ばれる Windows サービスが含まれます。 WBS は、"WinBio サービス"とも呼ばれます。 WBDI ドライバーは、WinBio サービスからの要求に応答します。 WBF には、Windows ログインのサポートも含まれています。

このドキュメントでは、WBDI がについて説明します。 WBS は、Windows sdk とは別に記載されています。

### <a name="span-idchoosingadrivermodelspanspan-idchoosingadrivermodelspanchoosing-a-driver-model"></a><span id="choosing_a_driver_model"></span><span id="CHOOSING_A_DRIVER_MODEL"></span>ドライバー モデルの選択

Windows 生体認証ドライバー インターフェイス (WBDI) で動作するためのドライバーを開発する際に、最初の選択肢は、どのドライバー モデルを使用します。

Ihv が Windows ユーザー モード ドライバー フレームワークを使用して、生体認証デバイス ドライバーを開発することをお勧めします (とも呼ば WUDF [UMDF](https://docs.microsoft.com/previous-versions/ff554928(v=vs.85))) と WinUSB I/O ターゲット。

次の図は、UMDF に基づく Windows 生体認証ドライバー インターフェイス (WBDI) ドライバーを Windows 7、Windows 生体認証フレームワーク (WBF) 生体認証のサポートに収める方法を示します。 生体認証のすべての操作については、Windows 生体認証サービス (WBS) へのクライアント アプリケーションによって決まります。 WBS は、WBDI インターフェイスを公開する生体認証デバイス ドライバーへの要求を送信します。

![生体認証ドライバーの内部アーキテクチャを示す図](images/bioarch.png)

前の図では、仕入先は、生体認証デバイス ドライバー DLL を提供します。

UMDF を使用して、ドライバーを開発する必要がない場合は、か WDM、KMDF ドライバーを使用して、WBDI を実装するために選択することもできますが、これは推奨されるドライバーの開発環境ではありません。

ドライバー上最も推奨される方法と、下部にある最も優先順位の WBDI、開発できるさまざまな方法を次に示します。

1.  WinUsb I/O ターゲット UMDF

2.  UMDF WinUsb またはカスタムの KMDF I/O ターゲットでカスタム KMDF フィルターを適用

3.  KMDF

4.  WDM (絶対に必要な場合のみ)

このドキュメントでは、UMDF を使用して、WBDI ベースのユーザー モードの USB 生体認証ドライバーを作成する方法について説明します。

 

 






---
title: NetAdapterCx クライアント ドライバーの構築
description: NetAdapterCx クライアント ドライバーの構築
ms.assetid: 0A6957B4-E63A-4687-B31E-064AE3A34936
keywords:
- NIC ドライバーの構築、NetAdapterCx クライアント ドライバーの構築
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: a340ed692cdf373b50c311aef8623e437422c353
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386375"
---
# <a name="building-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーの構築

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Visual Studio と Windows Driver Kit (WDK) の最新バージョンを取得するには、次を参照してください、[ハードウェア デベロッパー センター](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)します。

Visual Studio で新しい NetAdapter クライアント ドライバーを作成するのにには、次の手順を使用します。

1. Microsoft Visual Studio を開きます。 [ファイル] メニューで、次のように選択します。**新規 > プロジェクト**します。
2. **新しいプロジェクト > テンプレート > Visual C > Windows ドライバー > WDF**ダイアログ ボックスで、**カーネル モード ドライバー (KMDF) テンプレート**します。
3. ドライバーのプロパティ ページ ダイアログを開くには、次のように選択します。**プロジェクト > プロパティ**します。
4. **構成プロパティ > ドライバーの設定 > ネットワーク アダプター ドライバー**ダイアログ ボックスで、**ネットワーク アダプター クラスの拡張機能へのリンク**ドロップダウンに設定し、 **を[はい]** .
5. **構成プロパティ > ドライバーの設定 > ネットワーク アダプター ドライバー**ダイアログ ボックスで、**ネットワーク アダプターのメジャー バージョン**と**ネットワーク アダプターのマイナー バージョン**.
    1. NetAdapterCx の現在のバージョンは**1.3**します。
6. すべてのソース ファイル (または、一般的な/プリコンパイル済みヘッダー) は、次のヘッダーを追加します。

```C++
#include <ntddk.h>
#include <wdf.h>
#include <netadaptercx.h>
```

Visual Studio で新しい NetAdapter クライアント ドライバーを作成する方法を示すビデオを見るを参照してください、[ネットワーク アダプター クラスの拡張機能。最初には、ドライバー](https://aka.ms/netadapter/video2) Channel 9 のビデオ。

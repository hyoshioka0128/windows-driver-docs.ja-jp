---
title: NetAdapterCx クライアント ドライバーの構築
description: NetAdapterCx クライアント ドライバーの構築
ms.assetid: 0A6957B4-E63A-4687-B31E-064AE3A34936
keywords:
- NIC ドライバーの構築、NetAdapterCx クライアント ドライバーの構築
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e930e458cc336e1d5da77b088bf242b0bc98d68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580967"
---
# <a name="building-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーの構築

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Visual Studio と Windows Driver Kit (WDK) の最新バージョンを取得するには、次を参照してください、[ハードウェア デベロッパー センター](https://developer.microsoft.com/windows/hardware/windows-driver-kit)します。

Visual Studio で新しい NetAdapter クライアント ドライバーを作成するのにには、次の手順を使用します。

1. Microsoft Visual Studio を開きます。 [ファイル] メニューで、次のように選択します。**新規 > プロジェクト**します。
2. **新しいプロジェクト > テンプレート > Visual C > Windows ドライバー > WDF**ダイアログ ボックスで、**カーネル モード ドライバー (KMDF) テンプレート**します。
3. ドライバーのプロパティ ページ ダイアログを開くには、次のように選択します。**プロジェクト > プロパティ**します。
4. **構成プロパティ > ドライバーの設定 > ネットワーク アダプター ドライバー**ダイアログ ボックスで、**ネットワーク アダプター クラスの拡張機能へのリンク**ドロップダウンに設定し、 **を[はい]**.
5. **構成プロパティ > ドライバーの設定 > ネットワーク アダプター ドライバー**ダイアログ ボックスで、**ネットワーク アダプターのメジャー バージョン**と**ネットワーク アダプターのマイナー バージョン**.
    1. NetAdapterCx の現在のバージョンは**1.3**します。
6. すべてのソース ファイル (または、一般的な/プリコンパイル済みヘッダー) は、次のヘッダーを追加します。

```C++
#include <ntddk.h>
#include <wdf.h>
#include <netadaptercx.h>
```

Visual Studio で新しい NetAdapter クライアント ドライバーを作成する方法を示すビデオを見るを参照してください、[ネットワーク アダプター クラスの拡張機能。最初には、ドライバー](https://aka.ms/netadapter/video2) Channel 9 のビデオ。

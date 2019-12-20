---
title: NetAdapterCx クライアント ドライバーの構築
description: NetAdapterCx クライアント ドライバーの構築
ms.assetid: 0A6957B4-E63A-4687-B31E-064AE3A34936
keywords:
- NetAdapterCx クライアントドライバーの構築、NIC ドライバーの構築
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32612d7e98833b0ed5ff8e7cf5ab4c7265241419
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210786"
---
# <a name="building-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーの構築

最新バージョンの Visual Studio と Windows Driver Kit (WDK) を入手するには、[ハードウェアデベロッパーセンター](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)にアクセスしてください。

Visual Studio で新しい NetAdapter クライアントドライバーを作成するには、次の手順に従います。

1. Microsoft Visual Studio を開きます。 [ファイル] メニューの [**新しい > プロジェクト**] をクリックします。
2. [**新しいプロジェクト > テンプレート > Visual C++ > WINDOWS Driver > WDF** ] ダイアログボックスで、[**カーネルモードドライバー (kmdf) テンプレート**] を選択します。
3. [ドライバーのプロパティページ] ダイアログボックスを開くには、[**プロジェクト > プロパティ**] を選択します。
4. [**構成プロパティ] > [ドライバーの設定 > ネットワークアダプタードライバー** ] ダイアログボックスで、[**ネットワークアダプタークラス拡張**] ドロップダウンへのリンクを選択し、 **[はい]** に設定します。
5. [**構成プロパティ] > [ドライバーの設定 > ネットワークアダプタードライバー** ] ダイアログボックスで、[**ネットワークアダプターのメジャーバージョン**] と [**ネットワークアダプターのマイナーバージョン**] を選択します。
    1. NetAdapterCx の現在のバージョンは**2.0**です。
6. すべてのソースファイル (または、共通/プリコンパイル済みヘッダー) に次のヘッダーを追加します。

```C++
#include <ntddk.h>
#include <wdf.h>
#include <netadaptercx.h>
```

Visual Studio で新しい NetAdapter クライアントドライバーを作成する方法を示すビデオについては、Channel 9 の[最初のドライバー](https://aka.ms/netadapter/video2)ビデオを参照してください。

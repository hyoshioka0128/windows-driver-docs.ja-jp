---
title: グラフィックス アーキテクチャ (XDDM) でビデオのミニポート ドライバー
description: グラフィックス アーキテクチャ (Windows 2000 モデル) でビデオのミニポート ドライバー
ms.assetid: 663cbedb-6637-4d7c-86d0-70d962459856
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、グラフィック
- WDK のビデオのミニポートのアーキテクチャ
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: c43c8be8a8a6c288efc1bfefe80ae07caf2092ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386107"
---
# <a name="video-miniport-driver-in-the-graphics-architecture-windows-2000-model"></a>グラフィックス アーキテクチャ (Windows 2000 モデル) でビデオのミニポート ドライバー

次の図は、NT ベースのオペレーティング システムのグラフィックス サブシステム内で、ビデオのミニポート ドライバーを示します。

![nt ベースのオペレーティング システムのグラフィックス アーキテクチャを示す図](images/2vidarch.png)

各ビデオのミニポート ドライバーでは、ディスプレイ ドライバーのハードウェア レベルのサポートを提供します。 グラフィックス エンジンを呼び出して、ディスプレイ ドライバー [ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)基になるビデオのミニポート ドライバーからサポートを要求する関数。 **EngDeviceIoControl**、ミニポート ドライバーにビデオ ポート ドライバーを介して要求を送信する、I/O システム サービスを呼び出します。

ほとんどの状況で、ディスプレイ ドライバーがミニポート ドライバーを基になる頻度の低い要求された操作やできない操作を本当に時間が重要なサポートを提供しますが、ユーザーに表示されるタイム クリティカルな操作を実行します。割り込みまたは別のプロセスへのコンテキスト スイッチによって割り込まれました。

ディスプレイ ドライバーがデバイスの割り込みを処理できないと、ミニポート ドライバーのみがデバイスのメモリを設定し、ディスプレイ ドライバーの仮想アドレス空間にマップします。

ビデオ ポート ドライバーは、ビデオのミニポート ドライバーをサポートするために提供されるシステム提供のモジュールです。 ディスプレイ ドライバーとビデオのミニポート ドライバーの仲介役として機能します

NT ベースのオペレーティング システムのディスプレイ ドライバーの詳細については、次を参照してください。[表示 (Windows 2000 モデル) の概要](introduction-to-display--windows-2000-model-.md)と[表示ドライバー (Windows 2000 モデル)](display-drivers--windows-2000-model-.md)します。

 

 






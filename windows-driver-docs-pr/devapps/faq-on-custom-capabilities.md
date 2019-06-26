---
title: カスタムの機能に関する FAQ
description: ハードウェア サポート アプリ (HSA) とその他の機能との違いについては、カスタム機能を説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87bb8913c51f02798d3e17d7d1080dc94f325c4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369378"
---
# <a name="faq-on-custom-capabilities"></a>カスタムの機能に関する FAQ

## <a name="how-are-custom-capabilities-different-from-other-capabilities"></a>カスタムの機能はその他の機能からさまざまな方法

1. Microsoft パートナーは、カスタム機能を定義できます。
2. カスタムの機能をコンパイル時 Windows にビルドする必要はありません。
3. Windows では、アプリのインストール時に、カスタム機能を使用するアプリが承認されていることを確認します。  他の機能については、Windows ストア アプリの提出を受信すると、この検証が行われます。

## <a name="whats-the-difference-between-uwp-apps-with-custom-capabilities-and-device-companion-apps-dcas"></a>カスタムの機能を備えた UWP アプリとデバイス コンパニオン アプリ (Dca) の違いは何ですか。

|                           | **DCA**                                                  | **カスタムの機能を使った UWP アプリ**|
|---------------------------|----------------------------------------------------------|-------------------------------------|
|通信|デバイスのシナリオの API (イメージのキャプチャ、スキャンなど。)<br>デバイスのプロトコル (USB、HID など) の Api<br>ドライバーのアクセス権を顧客|                                                                              
|モデルを信頼します。|"Container"レベルで定義されています。<br>システムの OEM は、内部コンポーネント用のアプリを送信する必要があります。|システム レベルで定義されています。<br>システムの OEM は、内部コンポーネント用のアプリを送信する必要があります。|
|アプリの自動取得  |周辺機器の使用                                  |すべてのハードウェアの利用可能          |
|展開の依存関係    |WU:ドライバー パッケージ<br>ストア:App|WU:ドライバー パッケージ<br>ストア:App                  |
                                                                                                                                                                                                    
Dca の詳細については、次を参照してください。[デバイス アプリを Microsoft Store の概要](https://docs.microsoft.com/windows-hardware/drivers/devapps/getting-started)します。


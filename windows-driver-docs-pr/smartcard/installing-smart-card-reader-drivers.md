---
title: スマート カード リーダー ドライバーのインストール
description: スマート カード リーダー ドライバーのインストール
ms.assetid: 6e641718-d6d0-4f09-8935-6b381ad0c085
keywords:
- スマートカードドライバー WDK、インストール
- ベンダー提供のドライバー WDK スマートカード、インストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57f21e7052f5a3e621f67bad9f2d64c22295262b
ms.sourcegitcommit: 0d8592f210fad676c139f41fcf11d13130282e7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68427371"
---
# <a name="installing-smart-card-reader-drivers"></a>スマート カード リーダー ドライバーのインストール


## <span id="_ntovr_installing_smart_card_reader_drivers"></span><span id="_NTOVR_INSTALLING_SMART_CARD_READER_DRIVERS"></span>


このセクションでは、Microsoft Windows 用のスマートカードリーダードライバーに固有のインストール情報について説明します。

独自のリーダードライバーを提供するベンダーは、ドライバーの INF ファイルの[**Inf バージョンセクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)で、各ドライバーを**smartcardreader**セットアップクラスのメンバーにする必要があります。 また、ベンダーは、スマートカードサービスを適切に構成するためのセクションも追加する必要があります。 次に、例を示します。

```cpp
[Version]
Signature="$Windows NT$"
Class=SmartCardReader
ClassGuid={50DD5230-BA8A-11D1-BF5D-0000F805F530}

; ============ Add reg for all readers ===============

[Reader.Install.AddReg]
HKLM, Software\Microsoft\Cryptography\Calais\Readers,,,
HKLM, System\CurrentControlSet\Services\SCardSvr,Start,0x00010001,2
HKLM, System\CurrentControlSet\Services\CertPropSvc,Start,0x00010001,2
```

独自の UMDF リーダードライバーを提供するベンダーには、PnP フィルタードライバーが UMDF リフレクターの上に配置されるようにするためのレジストリ設定が必要です。 具体的には、ドライバーの INF ファイルでは、次のエントリが必要です。

```cpp
[Install.NT.Wdf]
UmdfKernelModeClientPolicy=AllowKernelModeClients
```

スマートカードリーダーのドライバーのインストールに関連する特別な要件は他にありません。

Windows でのデバイスのインストールに関する一般的な情報については、「[デバイスのインストールの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)」を参照してください。










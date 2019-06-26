---
title: スマート カード リーダー ドライバーのインストール
description: スマート カード リーダー ドライバーのインストール
ms.assetid: 6e641718-d6d0-4f09-8935-6b381ad0c085
keywords:
- スマート カードのドライバー WDK をインストールします。
- ベンダーから提供されたドライバー WDK のスマート カードをインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1689b0e29d2cf805324d5631e8c417cb43ab5d8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356702"
---
# <a name="installing-smart-card-reader-drivers"></a>スマート カード リーダー ドライバーのインストール


## <span id="_ntovr_installing_smart_card_reader_drivers"></span><span id="_NTOVR_INSTALLING_SMART_CARD_READER_DRIVERS"></span>


このセクションでは、Microsoft Windows 2000 およびそれ以降のバージョンのオペレーティング システムのスマート カード リーダーのドライバーに固有のインストール情報を提供します。

リーダーのドライバーを供給するベンダーがのメンバーには各ドライバーのする必要があります、 **SmartCardReader**セットアップでクラス、 [ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)ドライバーの INF ファイル。 ベンダーは、スマート カード サービスを適切に構成するセクションを追加もする必要があります。 次に、例を示します。

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

独自の UMDF リーダーのドライバーを供給するベンダーには、UMDF reflector の一番上に配置する PnP フィルター ドライバーを許可するレジストリ設定が必要があります。 具体的には、ドライバーの INF ファイルでこのエントリが必要です。

```cpp
[Install.NT.Wdf]
UmdfKernelModeClientPolicy=AllowKernelModeClients
```

スマート カード リーダーのドライバーのインストールに関連付けられているその他の特別な要件はありません。

Windows 2000 およびそれ以降のバージョンのオペレーティング システムでのデバイス インストールの詳細については、次を参照してください。[デバイス インストールの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)します。










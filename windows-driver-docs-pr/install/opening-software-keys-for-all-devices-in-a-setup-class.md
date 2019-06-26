---
title: セットアップ クラス内のすべてのデバイス用のソフトウェア キーを開く
description: セットアップ クラス内のすべてのデバイス用のソフトウェア キーを開く
ms.assetid: B601982E-FCD6-4932-813C-A68B2F15FC5C
keywords:
- ソフトウェア キー WDK デバイスのインストール、セットアップ クラスのすべてのデバイス用に開けません
- セットアップ クラス WDK デバイスのインストール、デバイスのソフトウェア キーを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71c3b5baffb5d9f08679ad64c399201e0b2003a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366648"
---
# <a name="opening-software-keys-for-all-devices-in-a-setup-class"></a>セットアップ クラス内のすべてのデバイス用のソフトウェア キーを開く


ユーザー モード アプリケーションを開くと、*ソフトウェア キー*デバイス セットアップ クラスで、すべてのデバイス用にする必要があります直接レジストリにアクセスできませんデバイス セットアップ クラスのサブキーの列挙。 レジストリ キーと同様にこのキーの名前と場所は、Windows の異なるバージョン間変更可能性があります。

安全に列挙し、デバイス セットアップ クラスのサブキーを開くと、これらの手順に従います。

1.  使用[ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)または[ **SetupDiGetClassDevsEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)指定したすべてのデバイスに関する情報のセットを取得するにはデバイス セットアップ クラス。

2.  使用[ **SetupDiEnumDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)セット内のすべてのデバイスを列挙します。

3.  使用[ **SetupDiOpenDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)を各デバイスにソフトウェア キーを開きます。 *KeyType* DIREG_DRV にパラメーターを設定する必要があります。

**注**  一部のデバイスが存在し、列挙でのデバイスの場合など、ソフトウェア キーがない、[プラグ アンド プレイ (PnP) manager](pnp-manager.md)がインストールされていませんが。

 

 

 






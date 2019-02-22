---
title: すべてのデバイス セットアップ クラスでのソフトウェア キーを開く
description: すべてのデバイス セットアップ クラスでのソフトウェア キーを開く
ms.assetid: B601982E-FCD6-4932-813C-A68B2F15FC5C
keywords:
- ソフトウェア キー WDK デバイスのインストール、セットアップ クラスのすべてのデバイス用に開けません
- セットアップ クラス WDK デバイスのインストール、デバイスのソフトウェア キーを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 603a1cdc57e3645c02848c997af5deba9bf6bf58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529323"
---
# <a name="opening-software-keys-for-all-devices-in-a-setup-class"></a>すべてのデバイス セットアップ クラスでのソフトウェア キーを開く


ユーザー モード アプリケーションを開くと、*ソフトウェア キー*デバイス セットアップ クラスで、すべてのデバイス用にする必要があります直接レジストリにアクセスできませんデバイス セットアップ クラスのサブキーの列挙。 レジストリ キーと同様にこのキーの名前と場所は、Windows の異なるバージョン間変更可能性があります。

安全に列挙し、デバイス セットアップ クラスのサブキーを開くと、これらの手順に従います。

1.  使用[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)または[ **SetupDiGetClassDevsEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551072)指定したすべてのデバイスに関する情報のセットを取得するにはデバイス セットアップ クラス。

2.  使用[ **SetupDiEnumDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551010)セット内のすべてのデバイスを列挙します。

3.  使用[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)を各デバイスにソフトウェア キーを開きます。 *KeyType* DIREG_DRV にパラメーターを設定する必要があります。

**注**  一部のデバイスが存在し、列挙でのデバイスの場合など、ソフトウェア キーがない、[プラグ アンド プレイ (PnP) manager](pnp-manager.md)がインストールされていませんが。

 

 

 






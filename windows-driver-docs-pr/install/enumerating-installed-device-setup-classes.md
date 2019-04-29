---
title: インストール済みのデバイス セットアップ クラスの列挙
description: インストール済みのデバイス セットアップ クラスの列挙
ms.assetid: 24F7600B-AA61-484a-83E9-E4C3FD2EAF17
keywords:
- WDK のデバイス セットアップ クラスがインストールされている列挙
- インストール済みのデバイス セットアップ クラス WDK
- デバイス セットアップ クラス、WDK をインストールを列挙します。
- デバイス セットアップ クラスを列挙する、WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73cf7ac20435bb3cd91edc88e7b1b22c433620eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386985"
---
# <a name="enumerating-installed-device-setup-classes"></a>インストール済みのデバイス セットアップ クラスの列挙


検出する、[デバイス セットアップ クラス](device-setup-classes.md)をシステムにインストールされている場合は、レジストリ キーに直接アクセスのデバイス セットアップ クラスを列挙できません。 レジストリ キーと同様にこれらのキーの形式と場所は、Windows の異なるバージョン間変更可能性があります。

安全に、インストール済みのデバイス セットアップ クラスを検出してセットアップ クラスのプロパティを変更し、次の手順に従います。

1.  使用[ **SetupDiBuildClassInfoList** ](https://msdn.microsoft.com/library/windows/hardware/ff550909)または[ **SetupDiBuildClassInfoListEx** ](https://msdn.microsoft.com/library/windows/hardware/ff550911)デバイス セットアップ クラスのセットを取得するには現在システムにインストールします。

2.  使用[ **SetupDiGetClassDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff551053)または[ **SetupDiGetClassDescriptionEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551058)インストール済みのセットアップの説明を取得するにはクラス。

3.  使用[ **SetupDiGetClassRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551097)セットアップ クラスのプロパティを照会し、 [ **SetupDiSetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552169)を設定するにはセットアップ クラスのプロパティ。

4.  使用[ **SetupDiOpenClassRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552065)または[ **SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)カスタム デバイスのレジストリの永続的なストレージにアクセスするにはクラスの設定をセットアップします。

 

 






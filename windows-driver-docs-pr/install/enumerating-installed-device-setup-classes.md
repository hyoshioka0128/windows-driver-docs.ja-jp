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
ms.openlocfilehash: 3293b81b496c2607b9b02346f0686e73927c8d4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379476"
---
# <a name="enumerating-installed-device-setup-classes"></a>インストール済みのデバイス セットアップ クラスの列挙


検出する、[デバイス セットアップ クラス](device-setup-classes.md)をシステムにインストールされている場合は、レジストリ キーに直接アクセスのデバイス セットアップ クラスを列挙できません。 レジストリ キーと同様にこれらのキーの形式と場所は、Windows の異なるバージョン間変更可能性があります。

安全に、インストール済みのデバイス セットアップ クラスを検出してセットアップ クラスのプロパティを変更し、次の手順に従います。

1.  使用[ **SetupDiBuildClassInfoList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolist)または[ **SetupDiBuildClassInfoListEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa)デバイス セットアップ クラスのセットを取得するには現在システムにインストールします。

2.  使用[ **SetupDiGetClassDescription** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptiona)または[ **SetupDiGetClassDescriptionEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa)インストール済みのセットアップの説明を取得するにはクラス。

3.  使用[ **SetupDiGetClassRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)セットアップ クラスのプロパティを照会し、 [ **SetupDiSetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)を設定するにはセットアップ クラスのプロパティ。

4.  使用[ **SetupDiOpenClassRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)または[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)カスタム デバイスのレジストリの永続的なストレージにアクセスするにはクラスの設定をセットアップします。

 

 






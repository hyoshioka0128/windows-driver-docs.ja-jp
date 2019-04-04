---
title: デバイスのソフトウェア キーを開く
description: デバイスのソフトウェア キーを開く
ms.assetid: CA9EC186-7991-4cc5-B49E-DFE87A13BCFA
keywords:
- ソフトウェア キーを開く、WDK デバイスのインストール
- ソフトウェア キー WDK のデバイスのインストールを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6dc84397a5f16a51fffa198b30cdc1d97f28ac1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571848"
---
# <a name="opening-a-devices-software-key"></a>デバイスのソフトウェア キーを開く


デバイスを直接開く必要がありますいない*ソフトウェア キー*します。 レジストリ キーと同様に場所またはこれらのキーの形式は、Windows の異なるバージョン間変更可能性があります。

**注**  対応するデバイスが検出された後にのみ、デバイスのソフトウェア キーを開く必要があります。 この手順の詳細については、[インストールされているデバイスを列挙する](enumerating-installed-devices.md)を参照してください。

 

デバイスのソフトウェア キーを開くには、次のガイドラインに従います。

-   既存のソフトウェア キーを開くには、次のように使用します。 [ **SetupDiOpenDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552079)します。 ソフトウェア キーを作成するには使用[ **SetupDiCreateDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff550973)します。 いずれの場合も、設定する必要があります、 *KeyType* DIREG_DRV パラメーター。

    **注**  設定する必要があります、 *samDesired*パラメーターを必要とされる最小限のアクセス許可。 KEY_ALL_ACCESS にこのパラメーターを設定する必要がありますできません。 レジストリへのアクセスのアクセス許可を指定する方法の詳細については、[レジストリのキーを安全にアクセスする](accessing-registry-keys-safely.md)を参照してください。

     

-   カーネル モードの呼び出し元が使用する必要があります[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)設定と、 *DevInstKeyType* PLUGPLAY_REGKEY_DRIVER パラメーター。

 

 






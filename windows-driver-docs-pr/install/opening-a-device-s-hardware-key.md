---
title: デバイスのハードウェア キーを開く.
description: デバイスのハードウェア キーを開く.
ms.assetid: FED22F37-D09C-4207-8C2C-FB6484A8D19D
keywords:
- ハードウェア キーを開く、WDK デバイスのインストール
- ハードウェア キー WDK デバイスのインストールを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07321f59c1d5d516edf98cf588e47d57044c0714
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532754"
---
# <a name="opening-a-devices-hardware-key"></a>デバイスのハードウェア キーを開く.


A*ハードウェア キー*デバイスに関する情報を格納しているデバイスに固有のレジストリ サブキーです。 デバイスのハードウェア キーを直接開く必要があります。 レジストリ キーと同様に場所またはこれらのキーの形式は、Windows の異なるバージョン間変更可能性があります。 

**注**  対応するデバイスが検出された後にのみ、デバイスのハードウェア キーを開く必要があります。 この手順の詳細については、次を参照してください。[インストールされているデバイスを列挙する](enumerating-installed-devices.md)します。

 

開くか、デバイスのハードウェア キーを作成、これらのガイドラインに従います。

-   既存のハードウェア キーを開くには、次のように使用します。 [ **SetupDiOpenDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552079)します。 ハードウェア キーを作成するには使用[ **SetupDiCreateDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff550973)します。 いずれの場合も、設定する必要があります、 *KeyType* DIREG_DEV パラメーター。

    **注**  設定する必要があります、 *samDesired*パラメーターを必要とされる最小限のアクセス許可。 KEY_ALL_ACCESS にこのパラメーターを設定する必要がありますできません。 レジストリへのアクセスのアクセス許可を指定する方法の詳細については、次を参照してください。[レジストリのキーを安全にアクセスする](accessing-registry-keys-safely.md)します。

     

-   カーネル モードの呼び出し元が使用する必要があります[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)設定と、 *DevInstKeyType* PLUGPLAY_REGKEY_DEVICE パラメーター。

 

 






---
title: デバイスのソフトウェア キーを開く
description: デバイスのソフトウェア キーを開く
ms.assetid: CA9EC186-7991-4cc5-B49E-DFE87A13BCFA
keywords:
- ソフトウェア キーを開く、WDK デバイスのインストール
- ソフトウェア キー WDK のデバイスのインストールを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0625240bf094b030caeae8ba7e267b399df33147
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366656"
---
# <a name="opening-a-devices-software-key"></a>デバイスのソフトウェア キーを開く


デバイスを直接開く必要がありますいない*ソフトウェア キー*します。 レジストリ キーと同様に場所またはこれらのキーの形式は、Windows の異なるバージョン間変更可能性があります。

**注**  対応するデバイスが検出された後にのみ、デバイスのソフトウェア キーを開く必要があります。 この手順の詳細については、次を参照してください。[インストールされているデバイスを列挙する](enumerating-installed-devices.md)します。

 

デバイスのソフトウェア キーを開くには、次のガイドラインに従います。

-   既存のソフトウェア キーを開くには、次のように使用します。 [ **SetupDiOpenDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)します。 ソフトウェア キーを作成するには使用[ **SetupDiCreateDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)します。 いずれの場合も、設定する必要があります、 *KeyType* DIREG_DRV パラメーター。

    **注**  設定する必要があります、 *samDesired*パラメーターを必要とされる最小限のアクセス許可。 KEY_ALL_ACCESS にこのパラメーターを設定する必要がありますできません。 レジストリへのアクセスのアクセス許可を指定する方法の詳細については、次を参照してください。[レジストリのキーを安全にアクセスする](accessing-registry-keys-safely.md)します。

     

-   カーネル モードの呼び出し元が使用する必要があります[ **IoOpenDeviceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)設定と、 *DevInstKeyType* PLUGPLAY_REGKEY_DRIVER パラメーター。

 

 






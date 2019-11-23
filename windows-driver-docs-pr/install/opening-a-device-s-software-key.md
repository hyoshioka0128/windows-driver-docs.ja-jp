---
title: デバイスのソフトウェア キーを開く
description: デバイスのソフトウェア キーを開く
ms.assetid: CA9EC186-7991-4cc5-B49E-DFE87A13BCFA
keywords:
- ソフトウェアキー WDK デバイスのインストール、開く
- ソフトウェアキーを開く WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31f5499785ed2c8894985d4e2408b6a663cddbf2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837384"
---
# <a name="opening-a-devices-software-key"></a>デバイスのソフトウェア キーを開く


デバイスの*ソフトウェアキー*を直接開くことはできません。 レジストリキーと同様に、これらのキーの場所または形式は、Windows のバージョンによって異なる場合があります。

デバイスのソフトウェアキーは、対応するデバイスが検出された後にのみ開く必要**が  ます**。 この手順の詳細については、「[インストールされているデバイスの列挙](enumerating-installed-devices.md)」を参照してください。

 

デバイスのソフトウェアキーを開くには、次のガイドラインに従ってください。

-   既存のソフトウェアキーを開くには、 [**Setupdiopendevregkey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)を使用します。 ソフトウェアキーを作成するには、 [**Setupdicreatedevregkey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)を使用します。 どちらの場合も、 *KeyType*パラメーターを DIREG_DRV に設定する必要があります。

    必要に応じて、 *Samdesired*パラメーターを必要な最小限のアクセス許可に設定する必要**が  ます**。 このパラメーターを KEY_ALL_ACCESS に設定することはできません。 レジストリアクセスのアクセス許可を指定する方法の詳細については、「[レジストリキーに安全](accessing-registry-keys-safely.md)にアクセスする」を参照してください。

     

-   カーネルモードの呼び出し元は、 [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)を使用して、 *devinstkeytype*パラメーターを PLUGPLAY_REGKEY_DRIVER に設定する必要があります。

 

 






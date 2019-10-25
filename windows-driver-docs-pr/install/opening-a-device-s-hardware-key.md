---
title: デバイスのハードウェア キーを開く
description: デバイスのハードウェア キーを開く
ms.assetid: FED22F37-D09C-4207-8C2C-FB6484A8D19D
keywords:
- ハードウェアキー WDK デバイスのインストール、開く
- ハードウェアキーを開く WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecee18dee8a40cf47582ae02ed33eb41edbeede8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837400"
---
# <a name="opening-a-devices-hardware-key"></a>デバイスのハードウェア キーを開く


*ハードウェアキー*は、デバイスに関する情報を含むデバイス固有のレジストリサブキーです。 デバイスのハードウェアキーを直接開くことはできません。 レジストリキーと同様に、これらのキーの場所または形式は、Windows のバージョンによって異なる場合があります。 

デバイスのハードウェアキーは、対応するデバイスが見つかった場合にのみ開く必要**が  ます**。 この手順の詳細については、「[インストールされているデバイスの列挙](enumerating-installed-devices.md)」を参照してください。

 

デバイスのハードウェアキーを開く、または作成するには、次のガイドラインに従ってください。

-   既存のハードウェアキーを開くには、 [**Setupdiopendevregkey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)を使用します。 ハードウェアキーを作成するには、 [**Setupdicreatedevregkey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)を使用します。 どちらの場合も、 *KeyType*パラメーターを DIREG_DEV に設定する必要があります。

    必要に応じて、 *Samdesired*パラメーターを必要な最小限のアクセス許可に設定する必要**が  ます**。 このパラメーターを KEY_ALL_ACCESS に設定することはできません。 レジストリアクセスのアクセス許可を指定する方法の詳細については、「[レジストリキーに安全](accessing-registry-keys-safely.md)にアクセスする」を参照してください。

     

-   カーネルモードの呼び出し元は、 [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)を使用し、 *devinstkeytype*パラメーターを PLUGPLAY_REGKEY_DEVICE に設定する必要があります。

 

 






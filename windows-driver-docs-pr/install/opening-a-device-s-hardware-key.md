---
title: デバイスのハードウェア キーを開く
description: デバイスのハードウェア キーを開く
ms.assetid: FED22F37-D09C-4207-8C2C-FB6484A8D19D
keywords:
- ハードウェア キーを開く、WDK デバイスのインストール
- ハードウェア キー WDK デバイスのインストールを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88ffaee894de83953551b0eae2462471e8db2f0c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365465"
---
# <a name="opening-a-devices-hardware-key"></a>デバイスのハードウェア キーを開く


A*ハードウェア キー*デバイスに関する情報を格納しているデバイスに固有のレジストリ サブキーです。 デバイスのハードウェア キーを直接開く必要があります。 レジストリ キーと同様に場所またはこれらのキーの形式は、Windows の異なるバージョン間変更可能性があります。 

**注**  対応するデバイスが検出された後にのみ、デバイスのハードウェア キーを開く必要があります。 この手順の詳細については、次を参照してください。[インストールされているデバイスを列挙する](enumerating-installed-devices.md)します。

 

開くか、デバイスのハードウェア キーを作成、これらのガイドラインに従います。

-   既存のハードウェア キーを開くには、次のように使用します。 [ **SetupDiOpenDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)します。 ハードウェア キーを作成するには使用[ **SetupDiCreateDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)します。 いずれの場合も、設定する必要があります、 *KeyType* DIREG_DEV パラメーター。

    **注**  設定する必要があります、 *samDesired*パラメーターを必要とされる最小限のアクセス許可。 KEY_ALL_ACCESS にこのパラメーターを設定する必要がありますできません。 レジストリへのアクセスのアクセス許可を指定する方法の詳細については、次を参照してください。[レジストリのキーを安全にアクセスする](accessing-registry-keys-safely.md)します。

     

-   カーネル モードの呼び出し元が使用する必要があります[ **IoOpenDeviceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)設定と、 *DevInstKeyType* PLUGPLAY_REGKEY_DEVICE パラメーター。

 

 






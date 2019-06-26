---
title: アップロード中のドライバーの動作
description: アップロード中のドライバーの動作
ms.assetid: a8edfd88-89b9-4759-b9b3-6f1ff2ae7fc9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d0ec626b2e419f877e0361c7d6d24468bf1870f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385029"
---
# <a name="driver-behavior-on-upload"></a>アップロード中のドライバーの動作


ドライバーの動作は、アップロードがで呼び出されている項目の種類によって異なります。

たとえば場合、 **IWiaTransfer::Upload** 「フラット ベッド」項目が呼び出される (項目が[ **WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category) WIA に設定されて\_カテゴリ\_ベッド)、「フラット ベッド」項目がデータ ストレージ項目ではないため、データのアップロードの厳密な意味が定義されていません。 ベンダーは通常、使用して、 **IWiaTransfer::Upload**その拡張機能または何らかの独自の方法で、デバイスと通信するアプリケーションを有効にします。

ただし場合、 **IWiaTransfer::Upload**がアプリケーションの呼び出しで最近作成されたアプリケーション項目で呼び出される**IWiaItem2::CreateChildItem**アップロードを新しい一部表す必要がありますデバイスの記憶域に保存する必要があるファイルなど、デバイスのデータ項目。

**IWiaTransfer**と**IWiaItem2**インターフェイスが、Microsoft Windows SDK ドキュメントに記載されています。

 

 





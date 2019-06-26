---
title: デバイスとドライバーのレジストリ ツリーとキー
description: デバイスとドライバーのレジストリ ツリーとキー
ms.assetid: 8f6ac7c1-f31a-4d14-8ba7-b432615db073
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0ffef196f84300f7f5e4002fd24b409d0c611ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387322"
---
# <a name="registry-trees-and-keys-for-devices-and-drivers"></a>デバイスとドライバーのレジストリ ツリーとキー


オペレーティング システム、ドライバー、およびデバイスのインストール コンポーネント、ドライバー、およびデバイスに関する情報をレジストリに格納します。 一般に、ドライバーとデバイスのインストール コンポーネントは、システムの再起動前後で保持する必要があるデータを格納するのにレジストリを使用する必要があります。 ドライバーのレジストリ情報にアクセスする方法については、次を参照してください。 [、ドライバーのレジストリを使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-the-registry-in-a-driver)します。

レジストリの内容は、常に信頼されていない、変更可能な情報として処理されます。 レジストリに情報を書き込みます、ドライバー コンポーネントの 1 つが別のコンポーネントが後でして読み取る場合と見なさないでください情報が変更されていないこと、その間にします。 レジストリから情報を読んだ後、ドライバー コンポーネントは、情報を使用する前に常に検証する必要があります。

レジストリの詳細については一般に、Microsoft Windows SDK のドキュメントを参照してください。

このセクションには、ドライバー、およびデバイスに関する情報を格納するレジストリ キーの使用方法を説明する次のトピックが含まれています。

[デバイスとドライバーのレジストリ ツリー](overview-of-registry-trees-and-keys.md)

[RunOnce のレジストリ キー](runonce-registry-key.md)

[DeviceOverrides レジストリ キー](deviceoverrides-registry-key.md)

ドライバーがプラグ アンド プレイ (PnP) などのシステムのルーチンを使用してレジストリ キーにアクセスする必要があります[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)または[ **IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey). ユーザー モードのセットアップ コンポーネントなどでデバイスのインストール機能を使用する必要があります[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)または[ **SetupDiOpenDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey). 使用して、レジストリに INF ファイルからアクセスできる[ **INF AddReg ディレクティブ**](inf-addreg-directive.md)します。

**重要な**  *ドライバーする必要がありますいないこれらのレジストリ ツリーとキーに直接アクセスします。* このセクションの情報はレジストリの説明のみがデバイスのインストールや構成の問題をデバッグします。

 

 

 






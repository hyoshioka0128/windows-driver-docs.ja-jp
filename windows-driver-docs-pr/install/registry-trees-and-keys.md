---
title: デバイスとドライバーのレジストリ ツリーとキー
description: デバイスとドライバーのレジストリ ツリーとキー
ms.assetid: 8f6ac7c1-f31a-4d14-8ba7-b432615db073
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3b34c6a8212ae3d440e4dedf77c73c628612b62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828718"
---
# <a name="registry-trees-and-keys-for-devices-and-drivers"></a>デバイスとドライバーのレジストリ ツリーとキー


オペレーティングシステム、ドライバー、およびデバイスのインストールコンポーネントには、ドライバーとデバイスに関する情報がレジストリに格納されます。 一般に、ドライバーとデバイスのインストールコンポーネントでは、システムの再起動の間に維持する必要があるデータを格納するために、レジストリを使用する必要があります。 ドライバーがレジストリ情報にアクセスする方法の詳細については、「[ドライバーでのレジストリの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-the-registry-in-a-driver)」を参照してください。

レジストリの内容は、常に信頼されていない変更可能な情報として扱う必要があります。 ドライバーコンポーネントのいずれかがレジストリに情報を書き込み、別のコンポーネントが後でそれを読み取る場合は、その間に情報が変更されていないと想定しないでください。 レジストリから情報を読み取った後は、使用する前にドライバーコンポーネントが常に情報を検証する必要があります。

一般的なレジストリの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

ここでは、ドライバーとデバイスに関する情報を格納するためのレジストリキーの使用方法について説明します。

[デバイスとドライバーのレジストリツリー](overview-of-registry-trees-and-keys.md)

[RunOnce レジストリキー](runonce-registry-key.md)

[DeviceOverrides レジストリキー](deviceoverrides-registry-key.md)

ドライバーは、 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)や[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)などのシステムルーチンを使用して、レジストリ内のプラグアンドプレイ (PnP) キーにアクセスする必要があります。 ユーザーモードセットアップコンポーネントでは、 [**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)や[**Setupdiopendevregkey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)などのデバイスインストール機能を使用する必要があります。 Inf [**AddReg ディレクティブ**](inf-addreg-directive.md)を使用して、inf ファイルからレジストリにアクセスできます。

**重要な**  *ドライバーは、これらのレジストリツリーおよびキーに直接アクセスできないようにする必要があります。* このセクションのレジストリ情報の説明は、デバイスのインストールまたは構成の問題をデバッグする場合にのみ使用します。

 

 

 






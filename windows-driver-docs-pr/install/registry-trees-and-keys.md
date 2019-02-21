---
title: レジストリ ツリーとデバイスとドライバーのキー
description: レジストリ ツリーとデバイスとドライバーのキー
ms.assetid: 8f6ac7c1-f31a-4d14-8ba7-b432615db073
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0b4db3865fd79e1f335ee8628bc673e9e5fd1ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556743"
---
# <a name="registry-trees-and-keys-for-devices-and-drivers"></a>レジストリ ツリーとデバイスとドライバーのキー


オペレーティング システム、ドライバー、およびデバイスのインストール コンポーネント、ドライバー、およびデバイスに関する情報をレジストリに格納します。 一般に、ドライバーとデバイスのインストール コンポーネントは、システムの再起動前後で保持する必要があるデータを格納するのにレジストリを使用する必要があります。 ドライバーのレジストリ情報にアクセスする方法については、次を参照してください。 [、ドライバーのレジストリを使用して](https://msdn.microsoft.com/library/windows/hardware/ff565537)します。

レジストリの内容は、常に信頼されていない、変更可能な情報として処理されます。 レジストリに情報を書き込みます、ドライバー コンポーネントの 1 つが別のコンポーネントが後でして読み取る場合と見なさないでください情報が変更されていないこと、その間にします。 レジストリから情報を読んだ後、ドライバー コンポーネントは、情報を使用する前に常に検証する必要があります。

レジストリの詳細については一般に、Microsoft Windows SDK のドキュメントを参照してください。

このセクションには、ドライバー、およびデバイスに関する情報を格納するレジストリ キーの使用方法を説明する次のトピックが含まれています。

[デバイスとドライバーのレジストリ ツリー](overview-of-registry-trees-and-keys.md)

[RunOnce のレジストリ キー](runonce-registry-key.md)

[DeviceOverrides レジストリ キー](deviceoverrides-registry-key.md)

ドライバーがプラグ アンド プレイ (PnP) などのシステムのルーチンを使用してレジストリ キーにアクセスする必要があります[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)または[ **IoOpenDeviceRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff549443). ユーザー モードのセットアップ コンポーネントなどでデバイスのインストール機能を使用する必要があります[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967)または[ **SetupDiOpenDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552079). 使用して、レジストリに INF ファイルからアクセスできる[ **INF AddReg ディレクティブ**](inf-addreg-directive.md)します。

**重要な**  *ドライバーする必要がありますいないこれらのレジストリ ツリーとキーに直接アクセスします。* このセクションの情報はレジストリの説明のみがデバイスのインストールや構成の問題をデバッグします。

 

 

 






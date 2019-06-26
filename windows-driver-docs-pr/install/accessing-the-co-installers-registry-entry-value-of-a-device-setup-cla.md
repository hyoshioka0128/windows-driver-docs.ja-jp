---
title: デバイス セットアップ クラスのアクセスの共同インストーラー レジストリ エントリの値
description: デバイス セットアップ クラスの共同インストーラー レジストリ エントリ値へのアクセス
ms.assetid: 731d29df-6fdd-4f25-9758-d7306fef7ec0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f611af9896f2481a11c3cd41086b16bf8a15bf1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386046"
---
# <a name="accessing-the-co-installers-registry-entry-value-of-a-device-setup-class"></a>デバイス セットアップ クラスの共同インストーラー レジストリ エントリ値へのアクセス


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)が含まれています、[デバイス セットアップ クラス プロパティ](accessing-device-setup-class-properties.md)クラス用にインストールされている共同インストーラーを表します。 統一されたデバイス プロパティのモデルを使用して、 [ **DEVPKEY_DeviceClass_ClassCoInstallers**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-classcoinstallers) [プロパティ キー](property-keys.md)をこのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティもサポートします。 ただし、Windows の以前のバージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 代わりに、これらのバージョンの Windows では、対応するシステム定義のレジストリ エントリの値を使用して、このプロパティを表します。 Windows の以前のバージョンとの互換性を維持するために Windows Vista およびそれ以降のバージョンもこの値はサポート システム定義のレジストリ エントリ。 ただし、Windows Vista およびそれ以降のバージョンでこれらのプロパティにアクセスするのにプロパティのキーを使用する必要があります。

プロパティのキーを使用して、Windows Vista およびそれ以降のバージョンのデバイス セットアップ クラスのプロパティにアクセスする方法については、次を参照してください。[にアクセスするデバイス クラスのプロパティ (Windows Vista 以降)](accessing-device-class-properties--windows-vista-and-later-.md)します。

Windows Server 2003、Windows XP、および Windows 2000 で設定またはデバイス セットアップ クラスに対する次のレジストリ エントリの値にアクセスする Windows レジストリの関数を使用して、このプロパティを取得できます。

**HLM\\システム\\CurrentControlSet\\コントロール\\CoDeviceInstallers\\{** <em>デバイス セットアップ クラス guid</em> **}** .

クラスの共同インストーラーを登録する方法の詳細については、次を参照してください。[クラス共同インストーラーを登録する](registering-a-class-co-installer.md)します。

 

 






---
title: デバイス セットアップ クラスのアイコン プロパティへのアクセス
description: デバイス セットアップ クラスのアイコン プロパティへのアクセス
ms.assetid: 082b23ee-8f5c-41ad-9bb1-1437b71aa921
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b2a8c1acb41e6d523314f84c9dee8d5bf89bb1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385122"
---
# <a name="accessing-icon-properties-of-a-device-setup-class"></a>デバイス セットアップ クラスのアイコン プロパティへのアクセス


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)が含まれています[デバイス セットアップ クラスのプロパティ](accessing-device-setup-class-properties.md)デバイス セットアップ クラスのアイコンのプロパティを表します。 統一されたデバイス プロパティのモデルを使用して、 [ **DEVPKEY_DeviceClass_Icon**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-icon) [プロパティ キー](property-keys.md)と[ **DEVPKEY_DeviceClass_IconPath** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-iconpath)をこれらのプロパティを表すプロパティのキー。

Windows Server 2003、Windows XP、および Windows 2000 は、これらのデバイス セットアップ クラスのプロパティを直接サポートされません。 ただし、Windows の以前のバージョンでは、デバイス セットアップ クラスのアイコンについての情報を取得する次のメカニズムをサポートしています。

-   呼び出す[ **SetupDiLoadClassIcon** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon)内のデバイス セットアップ クラスを小さいアイコンのインデックスを取得する、 *MiniIconIndex*出力パラメーター。 取得された小さいアイコンのインデックスを渡すことができますし、 [ **SetupDiDrawMiniIcon** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon)指定したデバイス コンテキストで取得したクラスのアイコンの小さいアイコンを描画するためにします。

-   呼び出し元のコンテキストで、デバイス セットアップ クラスに対する大きなアイコンの読み込みを大きなアイコン、呼び出し元にハンドルを返す SetupDiLoadClassIcon を呼び出します。

以前のバージョンの Windows、Windows Vista およびそれ以降のバージョンとの互換性は維持するために、これらのデバイス セットアップ クラスのアイコンにアクセスするメカニズムもサポートします。 ただし、Windows Vista およびそれ以降のバージョンでアイコンのプロパティにアクセスするのにプロパティのキーを使用する必要があります。

 

 






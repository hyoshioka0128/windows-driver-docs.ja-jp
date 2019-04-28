---
title: デバイス セットアップ クラスのアイコン プロパティへのアクセス
description: デバイス セットアップ クラスのアイコン プロパティへのアクセス
ms.assetid: 082b23ee-8f5c-41ad-9bb1-1437b71aa921
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65a13f7e5922ccd2ab98b60a58b2fd6a56077228
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382260"
---
# <a name="accessing-icon-properties-of-a-device-setup-class"></a>デバイス セットアップ クラスのアイコン プロパティへのアクセス


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)が含まれています[デバイス セットアップ クラスのプロパティ](accessing-device-setup-class-properties.md)デバイス セットアップ クラスのアイコンのプロパティを表します。 統一されたデバイス プロパティのモデルを使用して、 [ **DEVPKEY_DeviceClass_Icon**](https://msdn.microsoft.com/library/windows/hardware/ff542299) [プロパティ キー](property-keys.md)と[ **DEVPKEY_DeviceClass_IconPath** ](https://msdn.microsoft.com/library/windows/hardware/ff542303)をこれらのプロパティを表すプロパティのキー。

Windows Server 2003、Windows XP、および Windows 2000 は、これらのデバイス セットアップ クラスのプロパティを直接サポートされません。 ただし、Windows の以前のバージョンでは、デバイス セットアップ クラスのアイコンについての情報を取得する次のメカニズムをサポートしています。

-   呼び出す[ **SetupDiLoadClassIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff552053)内のデバイス セットアップ クラスを小さいアイコンのインデックスを取得する、 *MiniIconIndex*出力パラメーター。 取得された小さいアイコンのインデックスを渡すことができますし、 [ **SetupDiDrawMiniIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff551005)指定したデバイス コンテキストで取得したクラスのアイコンの小さいアイコンを描画するためにします。

-   呼び出し元のコンテキストで、デバイス セットアップ クラスに対する大きなアイコンの読み込みを大きなアイコン、呼び出し元にハンドルを返す SetupDiLoadClassIcon を呼び出します。

以前のバージョンの Windows、Windows Vista およびそれ以降のバージョンとの互換性は維持するために、これらのデバイス セットアップ クラスのアイコンにアクセスするメカニズムもサポートします。 ただし、Windows Vista およびそれ以降のバージョンでアイコンのプロパティにアクセスするのにプロパティのキーを使用する必要があります。

 

 






---
title: フレンドリ名と、デバイス セットアップ クラスのクラス名にアクセスします。
description: デバイス セットアップ クラスのフレンドリ名およびクラス名へのアクセス
ms.assetid: 52775fc6-1c52-4bed-a943-1afcee67e7e9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74ab777ca65ee4b911a603921ab4a6a061a697df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366442"
---
# <a name="accessing-the-friendly-name-and-class-name-of-a-device-setup-class"></a>デバイス セットアップ クラスのフレンドリ名およびクラス名へのアクセス


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)が含まれています[デバイス セットアップ クラスのプロパティ](accessing-device-setup-class-properties.md)フレンドリ名とクラス名のデバイス セットアップ クラスを表します。 統一されたデバイス プロパティのモデルを使用して、 [ **DEVPKEY_DeviceClass_Name**](https://msdn.microsoft.com/library/windows/hardware/ff542315) [プロパティ キー](property-keys.md)と[ **DEVPKEY_DeviceClass_ClassName** ](https://msdn.microsoft.com/library/windows/hardware/ff542272)をこれらのプロパティを表すプロパティのキー。

Windows Server 2003、Windows XP、および Windows 2000 は、これらのデバイス セットアップ クラスのプロパティもサポートします。 ただし、Windows の以前のバージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 代わりに、これらのバージョンの Windows では、次のメカニズムを使用して、対応するプロパティの情報を取得します。

-   呼び出す[ **SetupDiGetClassDescriptionEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551058)デバイス セットアップ クラスのフレンドリ名を取得します。

-   呼び出す[ **SetupDiClassNameFromGuid** ](https://msdn.microsoft.com/library/windows/hardware/ff550947)デバイス セットアップ クラスのクラス名を取得します。

以前のバージョンの Windows、Windows Vista およびそれ以降のバージョンとの互換性は維持するために、フレンドリ名と、デバイス セットアップ クラスのクラス名にアクセスするこれらのメカニズムもサポートします。 ただし、Windows Vista およびそれ以降のバージョンでこれらのプロパティにアクセスするのにプロパティのキーを使用する必要があります。

 

 






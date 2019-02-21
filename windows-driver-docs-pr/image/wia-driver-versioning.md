---
title: WIA ドライバーのバージョン管理
description: WIA ドライバーのバージョン管理
ms.assetid: 9ebd79ac-d742-4524-9573-5873f7a8ec37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77605791d26e2141e05924608fb1ddee30911a61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536993"
---
# <a name="wia-driver-versioning"></a>WIA ドライバーのバージョン管理


ドライバーから返されるバージョン フィールドでサポートされる WIA (またはレガシ ドライバー STI) のバージョンがレポート[ **IStiUSD::GetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543817)します。 通常、ドライバーは STI にこのフィールドを設定\_で定義されているバージョン、 *Sti.h*します。

STI の値、Windows Vista の Windows Driver Kit (WDK)\_バージョンが STI の値より大きい\_以前のオペレーティング システムのバージョン。 Windows Vista をサポートする必要がある場合は、ドライバーは、そのドライバーのバージョンの Windows Vista の値を持つ、 [IStream データ転送](istream-data-transfers.md)します。

新しい Windows Vista WIA モデルに準拠した、Windows Vista ドライバーが STI を返す必要があります\_バージョン\_から返されるバージョン フィールドで 3 **IStiUSD::GetCapabilities**します。

 

 





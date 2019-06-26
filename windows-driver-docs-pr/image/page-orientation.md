---
title: ページの向き
description: ページの向き
ms.assetid: fb28863a-920a-4b26-a652-fb255622824f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f34fb489d86d42c68e4b9aeb0c4b3f875cc5abd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376534"
---
# <a name="page-orientation"></a>ページの向き


WIA ミニドライバーことを確認します、WIA\_IP\_選択領域を現在の ORIENTATION プロパティ意見に同意します。 アプリケーションには、WIA の値が変更された場合\_IP\_向きを現在選択されているページ サイズ、ミニドライバーの有効なものは、WIA の値を変更する必要があります\_IP\_ページ\_ページ サイズ新しい向きの値をサポートするサイズ。

その場合[ **WIA\_IP\_向き**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-orientation) LANSCAPE、エクステントの設定は「反転します」に設定されている。 たとえば、アプリケーション設定 WIA\_IP\_ページ\_WIA をサイズ\_ページ\_、A4、ミニドライバーを設定する必要があります[ **WIA\_IP\_ページ\_幅**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-page-width) 11692 へと[ **WIA\_IP\_ページ\_高さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-page-height) 8267 にします。 (、ミニドライバーを設定する必要がありますも[ **WIA\_IP\_XEXTENT** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)と[ **WIA\_IP\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)適宜)。場合 WIA\_IP\_ページ\_WIA にサイズが設定されている\_ページ\_カスタム、スキャンするページの範囲の大きさは向きの設定は使用されません。

 

 





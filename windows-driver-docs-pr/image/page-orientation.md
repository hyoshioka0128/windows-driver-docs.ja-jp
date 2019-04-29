---
title: ページの向き
description: ページの向き
ms.assetid: fb28863a-920a-4b26-a652-fb255622824f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18814746f04783600801f5f2e60b19fc26f77867
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327868"
---
# <a name="page-orientation"></a>ページの向き


WIA ミニドライバーことを確認します、WIA\_IP\_選択領域を現在の ORIENTATION プロパティ意見に同意します。 アプリケーションには、WIA の値が変更された場合\_IP\_向きを現在選択されているページ サイズ、ミニドライバーの有効なものは、WIA の値を変更する必要があります\_IP\_ページ\_ページ サイズ新しい向きの値をサポートするサイズ。

その場合[ **WIA\_IP\_向き**](https://msdn.microsoft.com/library/windows/hardware/ff552625) LANSCAPE、エクステントの設定は「反転します」に設定されている。 たとえば、アプリケーション設定 WIA\_IP\_ページ\_WIA をサイズ\_ページ\_、A4、ミニドライバーを設定する必要があります[ **WIA\_IP\_ページ\_幅**](https://msdn.microsoft.com/library/windows/hardware/ff552636) 11692 へと[ **WIA\_IP\_ページ\_高さ**](https://msdn.microsoft.com/library/windows/hardware/ff552632) 8267 にします。 (、ミニドライバーを設定する必要がありますも[ **WIA\_IP\_XEXTENT** ](https://msdn.microsoft.com/library/windows/hardware/ff552661)と[ **WIA\_IP\_YEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552669)適宜)。場合 WIA\_IP\_ページ\_WIA にサイズが設定されている\_ページ\_カスタム、スキャンするページの範囲の大きさは向きの設定は使用されません。

 

 





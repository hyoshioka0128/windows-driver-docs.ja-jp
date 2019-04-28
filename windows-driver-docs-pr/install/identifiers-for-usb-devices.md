---
title: USB デバイスの識別子
description: USB デバイスの識別子
ms.assetid: 9597eae3-2aaf-4942-9d03-1b03bd12fcfd
keywords:
- デバイスの識別文字列 WDK、USB デバイス
- 識別文字列の WDK デバイス、USB デバイス
- 識別子の WDK デバイス、USB デバイス
- USB 識別子 WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46f092c8d3fcda890f0e14e3c97934dbff07e275
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377050"
---
# <a name="identifiers-for-usb-devices"></a>USB デバイスの識別子





このセクションでは、デバイス、ハードウェア、および USB デバイスによって生成された互換性のある識別子について説明します。

Windows オペレーティング システムでは、プリンターと大容量記憶装置の特殊な USB 識別子を生成するため、次のドキュメントには、2 つのグループに USB 識別子が分かれています。

[標準の USB 識別子](standard-usb-identifiers.md)

[特別な USB 識別子](special-usb-identifiers.md)

すべての USB デバイス、USB バス ドライバーには、USB デバイスとインターフェイスの記述子から取得した値から成る識別子の標準セットが生成されます。 最初の 2 つのセクションでは、上記には、標準の USB 識別子がについて説明します。 標準の USB 識別子だけでなく、大容量の記憶域とプリンター デバイス用のネイティブの Windows ドライバーはプリンターと記憶域デバイスに特別な関連性についての情報で構成される USB 識別子の個別セットを生成します。 これらの特殊な USB 識別子は、2 番目のセクションで説明します。

**注**  USB 識別子に埋め込まれている数値は 16 進形式で、Microsoft Windows 2000 以降、します。

 

 

 






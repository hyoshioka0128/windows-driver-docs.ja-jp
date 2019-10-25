---
title: WDM バージョンの特定
description: WDM バージョンの特定
ms.assetid: 7ed288d9-6447-4b08-baf2-e7b743654ebd
keywords:
- WDM ドライバー WDK カーネル、バージョン
- バージョン WDK WDM
- 互換性 WDK WDM
- クロスシステム互換性 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9c0602d202f47da2018dc8220f391cc5dac4842
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828367"
---
# <a name="determining-the-wdm-version"></a>WDM バージョンの特定





クロスシステムの WDM ドライバーでは、 [**IoIsWdmVersionAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiswdmversionavailable)ルーチンを使用して、実行されているシステムでサポートされている wdm のバージョンを確認する必要があります。 **IoIsWdmVersionAvailable**の参照ページには、WDM のバージョン番号の一覧が表示されます。

ドライバーが処理する必要がある WDM の相違点については、「 [Wdm バージョンの相違点](differences-in-wdm-versions.md)」を参照してください。

 

 





---
title: ベンダー提供のデバイスのインストール コンポーネント
description: ベンダー提供のデバイスのインストール コンポーネント
ms.assetid: d86bdf75-9726-4b44-8753-7e9c19e88a61
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cd34bcb744dfb7039600bf19ccecdf592216dde
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394112"
---
# <a name="vendor-provided-device-installation-components"></a>ベンダー提供のデバイスのインストール コンポーネント


このトピックでは、IHV および OEM によって提供されるデバイスのインストール コンポーネントについて説明します。

<a href="" id="driver-package"></a>ドライバー パッケージ  
A[ドライバー パッケージ](driver-packages.md)の Windows でサポートされるデバイスを指定する必要がありますが、すべてのソフトウェア コンポーネントで構成されます。 これらのコンポーネントを以下に示します。

-   [INF ファイル](overview-of-inf-files.md)デバイスとドライバーのインストールに関する情報を提供します。 詳細については、次を参照してください。 [INF ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers/hid/creating-an-inf-file)します。

-   A[カタログ ファイル](catalog-files.md)のデジタル署名を含む、[ドライバー パッケージ](driver-packages.md)します。 詳細については、次を参照してください。[デジタル署名](digital-signatures.md)します。

-   デバイスのドライバーです。

<a href="" id="drivers"></a>ドライバー  
ドライバーにより、ハードウェア デバイスと対話します。 Windows では、ドライバーのバイナリ ファイル (.sys) をコピー、%systemroot% を\\system32\\ドライバー ディレクトリ、デバイスがインストールされている場合。 ドライバーは、ほとんどのデバイスの必要があります。

詳細については、次を参照してください。[ドライバー モデルを選択する](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)します。

Windows のドライバーの詳細については、次を参照してください。 [Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index)します。

 

 






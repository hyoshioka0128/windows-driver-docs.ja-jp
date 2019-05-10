---
title: ベンダー提供のデバイスのインストール コンポーネント
description: ベンダー提供のデバイスのインストール コンポーネント
ms.assetid: d86bdf75-9726-4b44-8753-7e9c19e88a61
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd9ccabaafab72081086a69b9bcee7b834eaf6a4
ms.sourcegitcommit: 3a51ae8db61be0e25549a5527ea3143e3025e82f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65455015"
---
# <a name="vendor-provided-device-installation-components"></a>ベンダー提供のデバイスのインストール コンポーネント


このトピックでは、IHV および OEM によって提供されるデバイスのインストール コンポーネントについて説明します。

<a href="" id="driver-package"></a>ドライバー パッケージ  
A[ドライバー パッケージ](driver-packages.md)の Windows でサポートされるデバイスを指定する必要がありますが、すべてのソフトウェア コンポーネントで構成されます。 これらのコンポーネントを以下に示します。

-   [INF ファイル](overview-of-inf-files.md)デバイスとドライバーのインストールに関する情報を提供します。 詳細については、次を参照してください。 [INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff538378)します。

-   A[カタログ ファイル](catalog-files.md)のデジタル署名を含む、[ドライバー パッケージ](driver-packages.md)します。 詳細については、次を参照してください。[デジタル署名](digital-signatures.md)します。

-   デバイスのドライバーです。

<a href="" id="drivers"></a>ドライバー  
ドライバーにより、ハードウェア デバイスと対話します。 Windows では、ドライバーのバイナリ ファイル (.sys) をコピー、%systemroot% を\\system32\\ドライバー ディレクトリ、デバイスがインストールされている場合。 ドライバーは、ほとんどのデバイスの必要があります。

詳細については、次を参照してください。[ドライバー モデルを選択する](https://msdn.microsoft.com/library/windows/hardware/ff554652)します。

Windows のドライバーの詳細については、次を参照してください。 [Windows ドライバーの概要](https://msdn.microsoft.com/library/windows/hardware/ff554690)します。

 

 






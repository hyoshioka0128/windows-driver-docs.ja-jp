---
title: ベンダー提供のデバイスのインストール コンポーネント
description: ベンダー提供のデバイスのインストール コンポーネント
ms.assetid: d86bdf75-9726-4b44-8753-7e9c19e88a61
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4fa6b7aa475aae900ec78004268c82625ff6ff5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550527"
---
# <a name="vendor-provided-device-installation-components"></a>ベンダー提供のデバイスのインストール コンポーネント


このトピックでは、IHV および OEM によって提供されるデバイスのインストール コンポーネントについて説明します。

<a href="" id="driver-package"></a>ドライバー パッケージ  
A[ドライバー パッケージ](driver-packages.md)の Windows でサポートされるデバイスを指定する必要がありますが、すべてのソフトウェア コンポーネントで構成されます。 これらのコンポーネントを以下に示します。

-   [INF ファイル](inf-files.md)デバイスとドライバーのインストールに関する情報を提供します。 詳細については、[INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff538378)を参照してください。

-   A[カタログ ファイル](catalog-files.md)のデジタル署名を含む、[ドライバー パッケージ](driver-packages.md)します。 詳細については、[デジタル署名](digital-signatures.md)を参照してください。

-   デバイスのドライバーです。

<a href="" id="drivers"></a>ドライバー  
ドライバーにより、ハードウェア デバイスと対話します。 Windows では、ドライバーのバイナリ ファイル (.sys) をコピー、%systemroot% を\\system32\\ドライバー ディレクトリ、デバイスがインストールされている場合。 ドライバーは、ほとんどのデバイスの必要があります。

詳細については、[ドライバー モデルを選択する](https://msdn.microsoft.com/library/windows/hardware/ff554652)を参照してください。

Windows のドライバーの詳細については、[Windows ドライバーの概要](https://msdn.microsoft.com/library/windows/hardware/ff554690)を参照してください。

 

 






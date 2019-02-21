---
title: ネットワークの INF ファイルでモデルのセクション
description: ネットワークの INF ファイルでモデルのセクション
ms.assetid: 0340a875-ae5a-49c8-9498-1f8aba97e029
keywords:
- INF ファイルの WDK ネットワーク、モデルのセクション
- ネットワーク INF ファイル WDK、モデルのセクション
- モデルのセクションの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10b8ff2269083b12e2c92b1202f68c2266465c44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559208"
---
# <a name="models-section-in-a-network-inf-file"></a>ネットワークの INF ファイルでモデルのセクション





**モデル**ネットワーク INF ファイルのセクションは、ジェネリックに基づきます[ **INF モデル セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456)します。

**モデル**INF ファイルのセクションには、INF ファイルによってインストールされたコンポーネントの種類ごとに、次の形式のエントリが含まれています。

\[*device-description*= *install-section.name*, *hw-id*\[, *compatible-id*...\]

このエントリの詳細については、次を参照してください。 [INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff549520)します。

*Hw id* (とも呼ばれる、デバイス、ハードウェア、またはコンポーネント ID) アダプターのネットワーク アダプターによって、PnP マネージャーに指定されたハードウェア ID に一致する必要があります。

*Hw id*の後にアンダー スコア、および、製造元の名前または製品名、たとえば、プロバイダー名で構成する必要がありますコンポーネント ネットワーク ソフトウェア。

-   MS\_DLC

-   MS\_IBMDLC

A*プロバイダー名*INF ファイルのプロバイダーを識別します。 A*製造元名*ソフトウェア コンポーネントの製造元を識別します。 *製品名*ソフトウェア コンポーネントを識別します。

 

 






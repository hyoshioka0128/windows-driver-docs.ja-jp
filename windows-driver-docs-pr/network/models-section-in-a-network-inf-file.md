---
title: ネットワーク INF ファイル内の Models セクション
description: ネットワーク INF ファイル内の Models セクション
ms.assetid: 0340a875-ae5a-49c8-9498-1f8aba97e029
keywords:
- INF ファイルの WDK ネットワーク、モデルのセクション
- ネットワーク INF ファイル WDK、モデルのセクション
- モデルのセクションの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca1450d79b01141757a3af63c0e7bed1d8b32418
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382210"
---
# <a name="models-section-in-a-network-inf-file"></a>ネットワーク INF ファイル内の Models セクション





**モデル**ネットワーク INF ファイルのセクションは、ジェネリックに基づきます[ **INF モデル セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)します。

**モデル**INF ファイルのセクションには、INF ファイルによってインストールされたコンポーネントの種類ごとに、次の形式のエントリが含まれています。

\[*device-description*= *install-section.name*, *hw-id*\[, *compatible-id*...\]

このエントリの詳細については、次を参照してください。 [INF ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)します。

*Hw id* (とも呼ばれる、デバイス、ハードウェア、またはコンポーネント ID) アダプターのネットワーク アダプターによって、PnP マネージャーに指定されたハードウェア ID に一致する必要があります。

*Hw id*の後にアンダー スコア、および、製造元の名前または製品名、たとえば、プロバイダー名で構成する必要がありますコンポーネント ネットワーク ソフトウェア。

-   MS\_DLC

-   MS\_IBMDLC

A*プロバイダー名*INF ファイルのプロバイダーを識別します。 A*製造元名*ソフトウェア コンポーネントの製造元を識別します。 *製品名*ソフトウェア コンポーネントを識別します。

 

 






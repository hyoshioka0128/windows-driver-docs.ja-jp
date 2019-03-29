---
title: Microsoft Windows とシステム ファームウェアの関係
description: Microsoft Windows とシステム ファームウェアの関係
ms.assetid: 83a43e49-cb06-4007-88d0-88f024c22825
keywords:
- Windows ハードウェア エラー アーキテクチャ WDK、Windows、およびファームウェア
- WHEA WDK、Windows、およびファームウェア
- WDK WHEA、Windows、およびファームウェア ハードウェア エラー
- WDK WHEA、Windows、およびファームウェアのエラー
- ファームウェア WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51f8c275257ccac541203080295a9c6809e7fe00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571035"
---
# <a name="relationship-between-microsoft-windows-and-the-system-firmware"></a>Microsoft Windows とシステム ファームウェアの関係


Microsoft Windows オペレーティング システムとシステム ファームウェアの両方は、ハードウェア エラーの処理での重要な役割を果たします。 Windows ハードウェア エラー アーキテクチャ (WHEA) では、ハードウェア エラーの処理のタスクを投稿できます両方されるメソッドが向上します。 WHEA、に基づいて、ハードウェア プラットフォーム ベンダーが、ファームウェアまたはオペレーティング システムは、主要なハードウェア エラーのリソースを所有するかどうかを特定できます。 さらに、WHEA でファームウェアのコントロールを渡すハードウェア エラーのリソースに適切な場合に、オペレーティング システム。

オペレーティング システムは、可能な限りは、ハードウェア エラーのリソースの所有する必要があります。 ただし、システム ファームウェアは、ハードウェア エラーのリソースの標準化がないのため、これらのリソースのいくつかの管理を継続する必要があります。 複数のハードウェア エラー報告の標準は定義されているし、採用して、Microsoft では、オペレーティング システム管理の対象にするハードウェアのエラー処理機構の詳細と考えています。

 

 





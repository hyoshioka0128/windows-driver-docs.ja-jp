---
title: プリンターの INF ファイルで装飾
description: プリンターの INF ファイルで装飾
ms.assetid: 86ddca11-e2a9-44b8-8c42-313116fc580e
keywords:
- WDK の INF ファイルを印刷する装飾
- 追加のドライバー WDK プリンター
- 装飾の INF WDK
- INF モデル セクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3340d38b2982220d757a2c593a620e74fefd32a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560167"
---
# <a name="decorations-in-printer-inf-files"></a>プリンターの INF ファイルで装飾


プリンター デバイス セットアップ クラスは、異なるプロセッサ アーキテクチャ用のドライバーに対応する機能のデバイス クラスの間で一意です。 たとえば、x86 プリンター ドライバー (x86 から成る 1 つバイナリ) x64 に追加できるマシン。 この例では、ドライバーは、x64 で決して実行されず、x86 コンピューター - ポイント アンド プリントが x86 のサポートを提供しますクライアント。 プリンター ドライバーのアーキテクチャの別のクライアントと呼ばれる、ポイント アンド プリントをサポートするために追加される*追加のドライバー*します。 ポイント アンド プリントのについては、[ポイントと印刷の概要](introduction-to-point-and-print.md)を参照してください。

異なるプロセッサ アーキテクチャ用の追加のドライバーを読み込む必要がある (つまり、x86、x64、および Itanium アーキテクチャの)、Microsoft Windows Server 2003 SP1 以降では、プリンター クラスのインストーラーと Windows XP の 64 ビット バージョンと装飾を使用して、後で、 [ **INF モデル セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456)コンピューターのアーキテクチャを識別するためをドライバーのターゲット。

### <a name="inf-file-decorations-and-windows-versions"></a>INF ファイルの文字装飾と Windows のバージョン

プリンターの INF ファイルで装飾は、Windows XP で導入されました。 Windows XP と Windows Server 2003 では、文字装飾は省略可能です。 モデルの INF セクションで装飾を指定すると、現在のプロセッサ アーキテクチャに一致することです。

SP1 および Windows XP の 64 ビット バージョンの Windows Server 2003 以降では、装飾 INF モデルのセクションでは不要になった x64 の省略可能なドライバーです。これらのドライバーでする必要があります、INF モデルのセクションでは装飾を使用して、ターゲット コンピューターを示します。

[プリンター ドライバーの INF ファイルで装飾を使用する方法](how-to-use-decorations-in-inf-files-for-printer-drivers.md)

 

 





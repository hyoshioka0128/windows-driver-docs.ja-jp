---
title: Windows XP と Windows Vista 用にドライバー パッケージを 1 つ作成する
description: Windows XP と Windows Vista 用にドライバー パッケージを 1 つ作成する
ms.assetid: 5e350152-edd7-4afb-bcba-dd0217d0d17a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ef93623ad1ebafd020388dff2034c9a64381ad2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365546"
---
# <a name="creating-a-single-driver-package-for-windows-xp-and-windows-vista"></a>Windows XP と Windows Vista 用にドライバー パッケージを 1 つ作成する


Microsoft [Connect](https://go.microsoft.com/fwlink/p/?linkid=133880) Web サイトには、core ドライバーの更新プログラムの 2 つのグループが用意されています。

-   Windows オペレーティング システム (Windows Server 2003、Windows XP、Windows 2000 など)、Windows Vista より前の再頒布可能パッケージの更新により、ハードウェア製造元がこれらのオペレーティング システムをサポートするために必要な特定のファイルを組み込む.

-   Windows Vista 以降、別のパッケージにより、コアの最新のドライバー パッケージを発送するハードウェアの製造元。

両方の Windows XP (およびその他の Windows オペレーティング システムを Windows Vista より前) をサポートするために Windows Vista と同じのドライバー パッケージ内の以降のオペレーティング システム ハードウェアの製造元が、適切な再頒布可能パッケージを使用して、およびを INF を構築する必要がありますそれに応じて。

### <a name="no-redistributable-package"></a>再頒布可能パッケージに含まれない

場合、ドライバーは、(コア ドライバーの再配布する必要はありません) の場合は、ドライバーのコア コンポーネントのバージョンの Windows XP と Windows Vista の両方で動作、これらの手順に従います。

1.  引き続き Windows Vista では、Windows XP ドライバーを使用します。 変更する必要はありません。

2.  Windows Vista プレミアム ロゴの認定資格、Windows XP (およびその他の Windows オペレーティング システムを Windows Vista より前) の個別の INF インストール セクションが用意して、Windows Vista およびそれ以降のオペレーティング システム、および make、INF セクションの Windows Vista のインストールパッケージに注意してください。

### <a href="" id="redistributable-package-for-windows-operating-systems-earlier-than-win"></a> 再頒布可能パッケージの Windows オペレーティング システムの Windows Vista より前

場合は、Windows Vista の初期リリースでは、ドライバーが動作しますが、Windows Vista バージョンの Windows XP およびそれ以前のオペレーティング システムで動作するコア ドライバー コンポーネントを作成する必要があります (つまり、Windows Vista より前の Windows オペレーティング システムの配布必要) これらの手順に従います。

1.  Windows Vista、Windows XP (およびその他の Windows オペレーティング システムを Windows Vista より前) に個別の INF インストール セクションを作成 (以降)。

2.  INF を使用して、 **CoreDriverDependencies**と**CoreDriverSections**受信トレイのコアのドライバー パッケージを使用する INF ファイルの Windows Vista のセクションを強制的にディレクティブ。

3.  Windows オペレーティング システム Windows Vista より前にこれらのオペレーティング システム バージョンをサポートするために必要な再配布パッケージからファイルを決定します。

4.  ダウンレベルのサポートの必要なバイナリをドライバー パッケージに含めるし、Windows オペレーティング システムで Windows Vista より前のインストールのみコピーしています。

### <a name="windows-vista-redistributable-package"></a>Windows Vista の再頒布可能パッケージ

場合は、ドライバーでは、最初のリリースの Windows Vista と Windows XP (Windows Vista への再配布が必要です) の場合は、正しく動作を次の手順に従ってコア ドライバー パッケージの更新バージョンが必要です。

1.  Windows Vista、Windows XP (およびその他の Windows オペレーティング システムを Windows Vista より前) に個別の INF インストール セクションを作成し、後でします。

2.  ドライバー パッケージのサブディレクトリには、全体の Windows Vista の中核となるドライバー パッケージを含めます。

3.  使用して、 [ **INF CopyINF ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547317)中核となる更新されたドライバーをドライバー ストアにプリロードします。

4.  INF を使用して、 **InboxVersionRequired**=*&lt;中核となる更新されたドライバーのバージョン&gt;* core のドライバー パッケージの新しいバージョンのみを確実にディレクティブこのオプションを使用するとします。

5.  INF を使用して、 **CoreDriverDependencies**と**CoreDriverSections**ディレクティブを Windows Vista ドライバーが更新されたコアのドライバーが必要であるかを示します。

6.  場合、ドライバーの一部と同様に、インストールには、Windows オペレーティング システムを Windows Vista より前のセクションが、コアが含まれるドライバー パッケージから直接必要なファイルをコピーします。

 

 





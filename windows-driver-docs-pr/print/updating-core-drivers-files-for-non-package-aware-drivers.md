---
title: パッケージに対応していないドライバーのコアのドライバー ファイルを更新しています
description: パッケージに対応していないドライバーのコアのドライバー ファイルを更新しています
ms.assetid: ce5da376-edac-4cd1-8750-9981bb5b709d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c4e01fbef1146d184f1d1f9f114a93486862ff2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536456"
---
# <a name="updating-core-drivers-files-for-non-package-aware-drivers"></a>パッケージに対応していないドライバーのコアのドライバー ファイルを更新しています


ドライバーのコア コンポーネント以前の Windows オペレーティング システム Windows Vista、Windows Server 2003、Windows XP、Windows 2000 などよりは、Microsoft で使用できる[Connect](https://go.microsoft.com/fwlink/p/?linkid=133880) XPSDrv の個別パッケージとしての Web サイトUniDrv、および PostScript ドライバー。 各パッケージには、さまざまな再配布契約があります。 パッケージ内のファイルは、実際、Windows Vista では、対応するのと同じです。 ドライバー ファイルをアンパックするのには記載された手順に従います[Core ドライバーの更新パッケージを取得する](getting-the-updated-core-driver-package.md)します。 Core のドライバー パッケージを展開する場合、ドライバーの一部と同様に、独自のドライバー パッケージに必要なコアのドライバー ファイルに含まれます。 つまり、コア パッケージからドライバーのバイナリ ファイルをドライバー パッケージのメイン ディレクトリにコピーします。 これ、core のデジタル署名されたドライバー パッケージの整合性が中断されますが、Windows XP (および他の Windows オペレーティング システム Windows Vista より前) が有効になります、れているドライバーがないパッケージ core ドライバーの更新プログラムを活用するために注意してください。

変更されていないコア ドライバー パッケージは Windows Vista でのパッケージに対応したインストールを有効に、ドライバー パッケージ内の個別のサブディレクトリにも格納できるに注意してください。 つまり、Windows Vista と Windows XP の両方の 1 つのドライバー パッケージをリリースできます。 パッケージ内の INF ファイルには、パッケージをインストールするオペレーティング システムに基づいて、core のドライバー ファイルの適切なソースを選択する必要があります。 Windows vista の場合、INF ファイルは、ドライバー パッケージ内のサブディレクトリから変更されていないコア ドライバー パッケージをインストールする必要があります。 Windows xp では、INF ファイルは、パッケージのメイン ディレクトリから、再頒布可能パッケージのコアのドライバー ファイルをインストールする必要があります。

Windows vista の場合、コアのドライバー パッケージに分割することを回避し、コアのドライバー ファイルをドライバー パッケージの一部として直接参照しないでください。 それ以外の場合、パッケージが Windows Vista で正常にインストールすることがありますが、印刷システムが不安定になると回帰の機能を結果として使用することがあります。 このような問題を回避するには、Windows Vista と Windows XP の両方で正しくインストールされることを確認するには、広範なドライバー更新プログラム パッケージをテストします。

詳細については、次を参照してください。[単一ドライバー パッケージの Windows XP と Windows Vista を作成する](creating-a-single-driver-package-for-windows-xp-and-windows-vista.md)します。

 

 





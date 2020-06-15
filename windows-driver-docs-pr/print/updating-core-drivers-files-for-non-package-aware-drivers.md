---
title: パッケージ対応ではないドライバーのコア ドライバー ファイルを更新する
description: パッケージ対応ではないドライバーのコア ドライバー ファイルを更新する
ms.assetid: ce5da376-edac-4cd1-8750-9981bb5b709d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1dcff399ff3615dc64d7119406174dda4e9ceff
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756162"
---
# <a name="updating-core-drivers-files-for-non-package-aware-drivers"></a>パッケージ対応ではないドライバーのコア ドライバー ファイルを更新する

Windows Vista より前の windows オペレーティングシステム (windows Server 2003、Windows XP、Windows 2000 を含む) のコアドライバーコンポーネントは、XPSDrv、UniDrv、および PostScript ドライバー用の個別のパッケージとして Microsoft [Connect](https://go.microsoft.com/fwlink/p/?linkid=133880) Web サイトから入手できます。 各パッケージには、異なる再配布契約があります。 パッケージ内のファイルは、実際には、Windows Vista では対応するファイルと同じです。 ドライバーファイルをアンパックするには、「[更新されたコアドライバーパッケージを取得](getting-the-updated-core-driver-package.md)する」に記載されている手順に従います。 コアドライバーパッケージを展開したら、ドライバーの一部であるかのように、必要なコアドライバーファイルを独自のドライバーパッケージに含めます。 つまり、コアパッケージからドライバーパッケージのメインディレクトリにドライバーのバイナリファイルをコピーします。 これにより、デジタル署名されたコアドライバーパッケージの整合性が損なわれますが、Windows XP (および Windows Vista より前の Windows オペレーティングシステム) とパッケージを認識しないドライバーがコアドライバーの更新プログラムを利用できるようになります。

変更されていないコアドライバーパッケージは、Windows Vista でパッケージ対応インストールを有効にするために、ドライバーパッケージ内の別のサブディレクトリに保存することができます。 つまり、Windows Vista と Windows XP の両方に対して1つのドライバーパッケージをリリースできます。 パッケージ内の INF ファイルでは、パッケージをインストールするオペレーティングシステムに基づいて、コアドライバーファイルの適切なソースを選択する必要があります。 Windows Vista では、ドライバーパッケージのサブディレクトリから、変更されていないコアドライバーパッケージをインストールする必要があります。 Windows XP の場合、INF ファイルはパッケージのメインディレクトリから再頒布可能コアドライバーファイルをインストールする必要があります。

Windows Vista の場合は、コアドライバーパッケージを分割せずに、ドライバーパッケージの一部として直接コアドライバーファイルを参照しないようにしてください。 そうしないと、Windows Vista でパッケージが正しくインストールされているように見えますが、その結果、印刷システムが不安定になり、機能が低下する可能性があります。 このような問題を回避するには、ドライバーの更新パッケージを広範囲にわたってテストして、Windows Vista と Windows XP の両方に正常にインストールされていることを確認します。

詳細については、「 [WINDOWS XP および Windows Vista 用の単一のドライバーパッケージの作成](creating-a-single-driver-package-for-windows-xp-and-windows-vista.md)」を参照してください。

---
title: グラフィックスの計測値
description: グラフィックスの測定値では、グラフィックス ドライバーのフライティング時に、良性の初期化エラーがフィルターで除外されます。
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 2aca54633e6ebb4610f0e1d1a8a40cd8708b6f4b
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223992"
---
# <a name="graphics-measures"></a>グラフィックスの計測値

[Windows Display Driver Model](https://docs.microsoft.com/windows-hardware/drivers/display/roadmap-for-developing-drivers-for-the-windows-vista-display-driver-mo) では、ユーザーモードのディスプレイ ドライバーとカーネルモードのディスプレイ ドライバーを対にして提出することをハードウェア ベンダーに義務付けています。 ユーザーモードのディスプレイ ドライバーは保護された領域で実行されるため、ドライバーのバイナリ内でクラッシュが発生してもマシンがクラッシュすることはありません。 一方、カーネルモード ドライバーは、アクセスできるマシンの機能がユーザーモード ドライバーよりも多く、エラーが発生するとマシンがクラッシュすることがあります。 これらのドライバーが一体となって、OS やアプリケーションからのバイナリ情報を、人が判読できるビジュアルに変換してユーザーに表示します。 グラフィックス コンポーネントはオーディオ コンポーネントと連動することが多いため、それらのドライバーも[オーディオの測定値](audio-measures.md)で評価されます。

加えて、グラフィックスの測定値のいくつかでは、アプリケーションにおけるユーザーモードのクラッシュ回数と、それらのアプリケーションの使用時間がカウントされます。 その使用時間は年単位に正規化され、Microsoft はその結果を使用して、ユーザーがアプリケーションを 1 年間使用した場合に遭遇するクラッシュの予想回数を計算します。

グラフィックス ドライバーは表面化するシナリオの範囲が広く、フライトの母集団だけではすべてカバーできない可能性があります。 そのため一部の測定では、**エコシステム オーディエンス**を対象とすることで、より多くのデータを収集し、サンプリング ノイズを低減して、統計的有意性を高めています。 そうしたエコシステムの測定値の一部には、**標準オーディエンス**での対応する測定値が存在します。

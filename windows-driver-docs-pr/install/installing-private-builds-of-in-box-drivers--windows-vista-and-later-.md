---
title: 受信トレイのドライバーのプライベート ビルドをインストールします。
description: 受信トレイのドライバーのプライベート ビルドをインストールします。
ms.assetid: 89170dff-284d-4d82-953c-46792158fbe5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91a860de23de38a93ea415f076d99fa49c1bcb66
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341483"
---
# <a name="installing-private-builds-of-inbox-drivers"></a>受信トレイのドライバーのプライベート ビルドをインストールします。


Windows Vista 以降、オペレーティング システムは、インストールできるメカニズムのバージョンの Microsoft によって署名されたドライバーの更新を提供します。 Microsoft によって署名されたドライバーの選択値が大きいほど、それ以外の場合、または*ランク*、サード パーティによって署名されているドライバーよりもします。 受信トレイのドライバーのプライベート ビルドをインストールするドライバー開発者向け困難になります。

このセクションでは、ビルドし、Windows の既定のインストールに含まれているドライバーのプライベート ビルドをインストールする方法について説明します。 このようなドライバーと呼ばれる、"*受信トレイ*"ドライバー。

**注**  にこのしくみを理解するには、ドライバーは、Windows によるこの署名とその他の条件に基づいたドライバーのランクにデジタル署名を理解しておく必要があります。 ドライバーのデジタル署名の詳細については、次を参照してください。[ドライバーの署名](driver-signing.md)します。

 

次のトピックでは、オーバーライドする方法、既定値 rank の数値には、ドライバーの受信トレイのドライバーのプライベート ビルドをインストールできるようにについて説明します。

[受信トレイのドライバーのビルドでプライベートのインストールの概要](overview-of-installing-private-builds-of-in-box-drivers.md)

[受信トレイのドライバーのプライベート ビルドを作成します。](creating-a-private-build-of-an-in-box-driver.md)

[Windows ドライバーの署名を均等にランク付けを構成します。](configuring-windows-to-rank-driver-signatures-equally.md)

[ドライバー パッケージの更新バージョンをインストールします。](installing-the-updated-version-of-the-driver-package.md)

**重要な**   Windows 更新プログラムは、シグネチャがサード パーティ製のドライバーよりも優先順位を持つ、Microsoft によって署名されたドライバーによって異なります。 この優先順位をオーバーライドするシステムを構成するは、コンシューマーに正しいドライバーを提供する Windows 更新プログラムの機能を妨げることができます。 これにより、Windows Update により提供されるドライバーのインストールに失敗します。

 

 

 






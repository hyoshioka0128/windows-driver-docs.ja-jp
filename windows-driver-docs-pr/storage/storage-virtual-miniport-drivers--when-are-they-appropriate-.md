---
title: 記憶域仮想ミニポート ドライバーが、適切な場合
description: 記憶域仮想ミニポート ドライバーが、適切な場合
ms.assetid: 45b9eab9-15b8-4244-bd16-e8850211b8bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 184525d984acba8f2a99f1773b7adf0fb161c1c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354542"
---
# <a name="storage-virtual-miniport-drivers-when-are-they-appropriate"></a>記憶域仮想ミニポート ドライバー: 適切な場合


仮想ミニポート ドライバーは、完全に 1 つまたは複数のデバイスをシミュレートまたは制御するための独自のハードウェアを持ちませんがの I/O 要求をトランスポートとしてそのデバイス ドライバーを使用して別のデバイスと通信を行う場合に適しています。 たとえば、ランダム アクセス メモリ (RAM) を使用してデータを格納するディスク デバイスには、RAMDISK は通常呼び出されます。 これは、仮想のミニポート ドライバーの適切な使用の良い例です。 別の例をいくつかの種類のストレージ コマンドとデータの送受信への通信リンクを提供するネットワーク アダプターの使用となります。 ネットワーク アダプターが、そのハードウェアを制御する独自のデバイス ドライバーが仮想ミニポートが、ドライバー、および基になるハードウェアではなくとのみ通信します。

実際のハードウェア、たとえば、ホスト バス アダプターを管理するが直接ときに、仮想ミニポートは適していません。

 

 





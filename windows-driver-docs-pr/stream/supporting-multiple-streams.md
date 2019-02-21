---
title: 複数のストリームをサポートしています。
description: 複数のストリームをサポートしています。
ms.assetid: 89f79078-129a-44cc-8b7e-5f5c1c33a473
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネル、複数のストリーム
- ミニドライバー WDK Windows 2000 のカーネル、複数のストリームのストリーミング
- ミニドライバー WDK Windows 2000 カーネル ストリーミング、複数のストリーム
- 複数のストリーム WDK ストリーミング ミニドライバー
- ストリームの番号は、WDK のミニドライバーのストリーミングをサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 460dc4969c5937ba7a8b67461624e5e67328a9f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558589"
---
# <a name="supporting-multiple-streams"></a>複数のストリームをサポートしています。





ミニドライバーでサポートするストリームを説明します。 その[ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463) 、SRB への応答で、日常的な\_取得\_ストリーム\_情報要求。 **CommandData.StreamBuffer**を指す、 [ **HW\_ストリーム\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff559686)構造で、ミニドライバーを入力する必要があります、ストリームのサポートの説明です。

ハードウェア ベース\_ストリーム\_記述子構造体の始まりを[ **HW\_ストリーム\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff559690)構造体は、ストリームの数について説明します、ミニドライバーをサポートします。 配列が続く[ **HW\_ストリーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff559692)構造体、それぞれが個別のストリームをについて説明します。 クラス ドライバーは、各ハードウェアを使用して\_ストリーム\_情報を処理するために、 [KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584) − 暗証番号 (pin) の ID 型として、配列内のインデックスのプロパティ セット

ハードウェア ベースのデータ、ほとんどのミニドライバーの\_ストリーム\_記述子は、コンパイル時に固定されます。 その場合は、ミニドライバーは、静的なデータ構造を割り当てることができます。

ミニドライバーは、ハードウェアのトポロジのメンバーを介してそのストリーム間の接続のトポロジをについて説明します\_ストリーム\_ヘッダー。 クラスのドライバーでは、この構造体を使用して、処理、 [KSPROPSETID\_トポロジ](https://msdn.microsoft.com/library/windows/hardware/ff566598)ミニドライバーのプロパティの設定。

 

 





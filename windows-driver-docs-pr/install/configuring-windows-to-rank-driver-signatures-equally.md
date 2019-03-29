---
title: ドライバーの署名が同一にランク付けされる Windows の構成
description: ドライバーの署名が同一にランク付けされる Windows の構成
ms.assetid: 727ad66d-b8f3-4e22-b51f-af9571ae0ec8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6afc27ab997232703ecea67a4cd01e8b1dfc4d3d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579190"
---
# <a name="configuring-windows-to-rank-driver-signatures-equally"></a>ドライバーの署名が同一にランク付けされる Windows の構成


[AllSignersEqual グループ ポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)コントロール[Windows がドライバーにランク付け](how-setup-ranks-drivers.md)サード パーティ ベンダーによって署名されているドライバーと Microsoft によって署名されています。 AllSignersEqual のグループ ポリシーを有効にすると、Windows はデバイスに最適なものであるドライバーを選択する際にすべての Microsoft 署名の種類とランクが等しいとサード パーティの署名を表示します。

**注**  で Windows Vista および Windows Server 2008 では、 **AllSignersEqual**グループ ポリシーが既定で無効になっています。 Windows 7 以降、このグループ ポリシーは既定で有効にします。

 

AllSignersEqual のグループ ポリシーを有効にした後は、AllSignersEqual のグループ ポリシーを無効にするまでに、この構成の変更が ターゲット システムのすべての後続のドライバーのインストールに適用されます。

詳細を構成する方法については、 **AllSignersEqual**同様に、ランクのドライバーの署名をグループ ポリシーを参照してください[AllSignersEqual グループ ポリシー (Windows Vista 以降)](allsignersequal-group-policy--windows-vista-and-later-.md)します。

 

 






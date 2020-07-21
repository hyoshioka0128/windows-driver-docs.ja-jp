---
title: ドライバーの署名が同一にランク付けされる Windows の構成
description: ドライバーの署名が同一にランク付けされる Windows の構成
ms.assetid: 727ad66d-b8f3-4e22-b51f-af9571ae0ec8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7bb2a3138719b5f0a46d26bc521784a540f84af
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557795"
---
# <a name="configuring-windows-to-rank-driver-signatures-equally"></a>ドライバーの署名が同一にランク付けされる Windows の構成


[AllSignersEqual グループポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)は、Microsoft によって署名されたドライバーと、サードパーティベンダーによって署名されたドライバーを[Windows がどのようにランク](how-setup-ranks-drivers--windows-vista-and-later-.md)付けするかを制御します。 AllSignersEqual グループポリシーが有効になっている場合、Windows では、デバイスに最適なドライバーを選択すると、Microsoft の署名の種類とサードパーティの署名がすべてランクに一致していることが表示されます。

**メモ**   Windows Vista および Windows Server 2008 では、 **AllSignersEqual**グループポリシーは既定で無効になっています。 Windows 7 以降では、このグループポリシーは既定で有効になっています。

 

AllSignersEqual グループポリシーを有効にした後、AllSignersEqual グループポリシーを無効にするまで、この構成の変更は、ターゲットシステム上の後続のすべてのドライバーのインストールに適用されます。

**AllSignersEqual**グループポリシーを構成してドライバーの署名を均等に順位付けする方法の詳細については、「 [AllSignersEqual グループポリシー (Windows Vista 以降)](allsignersequal-group-policy--windows-vista-and-later-.md)」を参照してください。

 

 






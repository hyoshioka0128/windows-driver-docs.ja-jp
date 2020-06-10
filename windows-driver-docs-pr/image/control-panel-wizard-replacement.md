---
title: コントロール パネル ウィザードの置換
description: コントロール パネル ウィザードの置換
ms.assetid: d4a418b6-a9f9-41c4-99a9-20992abe80e9
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 471d13605cac9d4d059134a4107b86ab9af1118d
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638420"
---
# <a name="control-panel-wizard-replacement"></a>コントロール パネル ウィザードの置換

ドライバーのアイコン (コントロールパネル、スキャナー、カメラ) をダブルクリックすると、ベンダーの UI ではなく、既定の UI スキャナーとカメラウィザードが表示されます。

このウィザードは、コモンダイアログと同じメカニズムを使用して置き換えることはできません。 コントロールパネルからベンダ UI を表示することができます。

コントロールパネルからベンダの UI を表示するには、次の操作を行う必要があります。

- 取得したアプリケーションを、このデバイスの既定の永続的なイベントハンドラーとして登録します。

- カスタムウィザードを作成します。

カスタムウィザードと、 [**Iwievicedialog Iextension::D**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))インターフェイスを使用して置換したダイアログの間にはリレーションシップがありません。

コントロールパネルのアイコンは、常に Windows Me と Windows XP のウィザードに既定で設定されることに注意してください。

既定の WIA \_ イベントスキャンイメージのイベントハンドラーを表示するには、ユーザーが右クリックして [スキャン] を明示的に選択する必要があり \_ \_ ます。

マイコンピューターでは、この逆の場合は、ユーザーがデバイスアイコンをダブルクリックしたときに使用される既定のハンドラーが選択されます。

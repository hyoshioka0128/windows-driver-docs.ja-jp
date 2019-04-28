---
title: コントロール パネル ウィザードの置換
description: コントロール パネル ウィザードの置換
ms.assetid: d4a418b6-a9f9-41c4-99a9-20992abe80e9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2846a1ad9d6d07224ef53210c52947557eead4b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368557"
---
# <a name="control-panel-wizard-replacement"></a>コントロール パネル ウィザードの置換





ベンダーの UI ではなく (から、コントロール パネルの スキャナーとカメラ)、ドライバーのアイコンがダブルクリックすると、既定の UI スキャナーとカメラ ウィザードが表示されます。 このウィザードは、同じメカニズムを使用してコモン ダイアログとして置き換え可能ではありません。 コントロール パネルからベンダ UI を表示することになります。

必要があります、コントロール パネルから、ベンダーの UI を表示するには。

-   自分のデバイスの既定の永続的なイベント ハンドラーとして、購入アプリケーションを登録します。

-   カスタム ウィザードを記述します。

関係がありませんすべてのカスタム ウィザードとダイアログ ボックスを使用してを置き換える、 [ **IWiaUIExtension::DeviceDialog** ](https://msdn.microsoft.com/library/windows/hardware/ff545069)インターフェイス。 ただし、注意してください。 コントロール パネルのアイコンはウィザードでは、Windows XP と Windows Me は、常に既定します。 ユーザーが右クリックし、既定 WIA を表示するには、明示的にスキャンを選択する必要があります\_イベント\_スキャン\_イメージ イベント ハンドラー。 マイ コンピューター、その逆が true であります。選択した任意の既定のハンドラーをユーザーがデバイスのアイコンをダブルクリックしたときに使用する 1 つとなります。

 

 





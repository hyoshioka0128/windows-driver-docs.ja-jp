---
title: システム電源状態変更の防止
description: システム電源状態変更の防止
ms.assetid: a744dfe7-d756-45c3-8fdf-7a403f6cde36
keywords:
- 変更されないように、システム電源の状態 WDK カーネル
- 状態遷移の WDK 電源管理
- PoRegisterSystemState
- PoSetSystemState
- PoUnregisterSystemState
- 作業の状態の WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e4397dae61f352ee8fb678356974d22d9f0dbfd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369129"
---
# <a name="preventing-system-power-state-changes"></a>システム電源状態変更の防止





ドライバーでは、システム電源ポリシーを直接設定できない、ですが、電源マネージャーは、ドライバーが稼働状態からシステム遷移を防ぐ次の 3 つのルーチンを提供します。[**PoSetSystemState**](https://msdn.microsoft.com/library/windows/hardware/ff559768)、 [ **PoRegisterSystemState**](https://msdn.microsoft.com/library/windows/hardware/ff559731)、および[ **PoUnregisterSystemState**](https://msdn.microsoft.com/library/windows/hardware/ff559794)します。

呼び出して**PoRegisterSystemState**または**PoSetSystemState**ドライバーは、ユーザーが存在するか、ドライバーでは、システムまたは表示の使用が必要な電源マネージャーに通知できます。

**PoRegisterSystemState**継続的なビジー状態を登録するためのドライバーを使用します。 使用される、ドライバーは後でその設定を変更ハンドルを返します。 状態の登録を有効になっている限り、電源マネージャーしようとしませんシステムをスリープ状態を格納します。 ドライバーが呼び出すことによって、状態の登録をキャンセル**PoUnregisterSystemState**します。

**PoSetSystemState**ドライバーが同じ条件 (存在するユーザー、システムで必要な必要な表示) の電源マネージャーに通知しますが、この設定は、連続することはありません。 再起動、指定された条件に関連付けられている、アイドル状態のカウント ダウンの影響があります。

これらのルーチンを使用して、ドライバーできますが呼び出されないように多くの場合、作業の状態から遷移をすべてではありません。 電源マネージャー常にシャット ダウン、システム電源の停電が近づいているとき、またはユーザーが明示的にシャット ダウンを要求します。

 

 





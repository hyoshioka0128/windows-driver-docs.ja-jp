---
title: ユーザー モード関数
description: ユーザー モード関数
ms.assetid: 1faa04b1-0bf0-494c-b55f-5c90c259c8f5
keywords:
- フィードバックのドライバー WDK を非表示に、ユーザー モードの機能を強制します。
- ユーザー モード関数 WDK フォース フィードバック
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b696c45a8c3026af38850de3d1c7fa66ab3eb53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552620"
---
# <a name="user-mode-functions"></a>ユーザー モード関数





DirectInput フォース フィードバック有効のドライバーのインスタンスを作成しますに格納されている CLSID でという名前のオブジェクトを作成して、 **OEMForceFeedback**ジョイスティックの種類のサブキーのレジストリ サブキー。

DirectInput を使用してアプリケーションには、OLE ロードしない必要があります、ため、効果のドライバーが OLE 固有の動作に依存しないように注意してあります。 たとえば、DirectInput を使用してアプリケーションに依存できませんを呼び出す、**自身で**メソッド。 DirectInput は、有効のドライバー オブジェクトのインスタンスを作成する標準の COM の操作を実行します。 次の効果のドライバーの実装にこれが必要にのみ表示される効果を説明します。

DirectInput は、最後の効果ドライバー オブジェクトを解放した後、FreeLibrary 効果ドライバ DLL の手動で実行します。 そのため、効果ドライバ DLL は、有効のドライバー オブジェクトに関連付けられていないその他のリソースを作成する場合は手動で意図的にできないようにすることから FreeLibrary DLL 参照カウントを増やす LoadLibrary 自体DirectInput を途中で、DLL をアンロードします。

具体的には、効果ドライバ DLL は、ワーカー スレッドを作成する場合、効果のドライバーする必要がありますこの操作を実行人為的な LoadLibrary のワーカー スレッドが存在する限り。 ワーカー スレッドが不要になった場合 (たとえば、として、最後の効果ドライバー オブジェクトからの通知時に破棄される)、ワーカー スレッドは、DLL の参照カウントをデクリメントし、スレッドを終了する FreeLibraryAndExitThread メソッドを呼び出す必要があります。

DirectInput によって使用されるマグニチュードと向上のすべての値は、uniform 線形範囲全体。 物理デバイスで、非直線性は、アプリケーションが線形のデバイスを認識するように、デバイス ドライバーによって処理する必要があります。

ユーザー モードで公開されているフィードバック関数の強制、 [IDirectInputEffectDriver](https://msdn.microsoft.com/library/windows/hardware/ff540050)フォース フィードバック効果ドライバー DLL によってインターフェイスを実装する必要があります。 これらの関数の詳細については、IDirectInputEffectDriver を参照してください。

 

 





---
title: フィルター ドライバーのアンロード
description: フィルター ドライバーのアンロード
ms.assetid: e7ef209f-ab61-4644-a641-2fef09023a24
keywords:
- フィルター ドライバー WDK ネットワーク、アンロード
- NDIS フィルター ドライバー WDK、アンロード
- フィルター ドライバーをアンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e0a3406d78d85bb7292fd2156194defa40ff97c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574034"
---
# <a name="unloading-a-filter-driver"></a>フィルター ドライバーのアンロード





NDIS フィルター ドライバーに関連付けられているドライバー オブジェクトを指定します、 [*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)というルーチン*FilterDriverUnload*します。 システムを呼び出すことができます、 *FilterDriverUnload*ルーチンとフィルター ドライバーのサービスが削除されているすべてのミニポート アダプター。

[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ドライバー固有のリソースを解放する必要があります。 フィルター ドライバーを作成したすべてのデバイス オブジェクトを破棄する必要があります。 システムは、後にドライバー アンロード操作を完了できる*FilterDriverUnload*を返します。

アンロード関数の機能は、ドライバー固有です。 一般的な規則として[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ドライバーの初期化中に実行された操作を元に戻す必要があります。 ドライバーの初期化の詳細については、[フィルター ドライバーの初期化](initializing-a-filter-driver.md)を参照してください。

フィルター ドライバーを呼び出す必要があります、 [ **NdisFDeregisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff561800)関数[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)します。 **NdisFDeregisterFilterDriver**呼び出し[ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)このフィルター ドライバーに関連付けられているすべてのフィルターが現在アタッチされているモジュールをデタッチします。

アンロードのフィルター ドライバーの詳細については、[ドライバー スタックを停止する](stopping-a-driver-stack.md)を参照してください。

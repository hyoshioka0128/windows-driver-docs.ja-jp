---
Description: Handling the Entry and Exit Points
title: エントリ ポイントと終了ポイントの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fe426b874ad0f17cac893c3d4508c9a37026bc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578957"
---
# <a name="handling-the-entry-and-exit-points"></a>エントリ ポイントと終了ポイントの処理


デバイスがドライバーのホストのプロセスで読み込まれるたびに、ユーザー モード ドライバー フレームワーク (UMDF) は、デバイス オブジェクトを追加します。 たびに、フレームワークは、オブジェクトを追加します。、メソッドを呼び出すと、、 **IDriverEntry**インターフェイス。 これらのメソッドは、CDriver クラスで表示されます。 次の表では、このクラスに含まれるメソッドについて説明します。

| メソッド                           | 説明                            |
|----------------------------------|----------------------------------------|
| **IDriverEntry::OnDeinitialize** | 必要なクリーンアップ操作を実行します。 |
| **IDriverEntry::OnDeviceAdd**    | システムには、新しいデバイスを追加します。       |
| **IDriverEntry::OnInitialize**   | ドライバーの初期化を処理します。         |

 

WpdHelloWorldDriver、 **OnDeviceAdd**メソッドが意味のある作業ができる唯一の方法、 **OnInitialize**メソッド S を単純に返します\_[ok] と**OnDeinitialize**メソッドに値を返しません。

コードを**OnDeviceAdd**メソッドは、次の手順を完了します。

1.  デバイスのコールバック オブジェクトを作成します。
2.  WDF デバイスを作成します。
3.  WpdBaseDriver オブジェクトを作成し、WDF デバイス オブジェクトに割り当てられます。
4.  キューのコールバック オブジェクトを作成します。
5.  既定のキューを作成します。

CDriver も実装**IObjectCleanup::OnCleanup**、中に WDF デバイス オブジェクトによって保持されている WpdBaseDriver オブジェクトへの参照を解放するコードを含む**OnDeviceAdd**します。

各インターフェイスとそのメソッドの詳細については、次を参照してください。、 [UMDF](https://go.microsoft.com/fwlink/p/?linkid=153678)ドキュメント。

 

 





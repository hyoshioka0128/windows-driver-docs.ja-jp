---
title: アカウントの受信イベントと削除イベントを処理するためのベスト プラクティス
description: アカウントの受信イベントと削除イベントを処理するためのベスト プラクティス
ms.assetid: e299a920-a27e-4832-b81d-1562f86f37e2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71fbe660d79a3e47cca3c290e2974ac3a9801d3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392986"
---
# <a name="best-practices-for-handling-account-arrival-and-removal-events"></a>アカウントの受信イベントと削除イベントを処理するためのベスト プラクティス


モバイル ブロード バンド アカウントを追加またはブロード バンドのモバイル アプリの有効期間中に削除できます。 これは、追加または削除のハードウェア、暗証番号 (pin) のロックを解除、または SIM スワップによって発生できます。 到達またはアカウントの削除は、多くの場合に一時的なものです。 これらのイベントの適切な処理は、アプリケーションの使いやすさに大きな影響を与えます。 次のベスト プラクティスは、アカウントの削除と到着のイベントの処理に適用されます。

-   すぐに上げないでくださいエラー ダイアログが使用されているアクティブなアカウントが削除されたとき。

-   ユーザーのハードウェアが削除されているとは限りません。 ドライバーまたはバスの動作によって、コンピューターのスリープ/再開中にはハードウェアを一時的に利用できない可能性があります。

-   呼び出さずに、開始アカウントの監視オブジェクトを解放しないその[**停止**](https://msdn.microsoft.com/library/windows/apps/hh770606)メソッド最初。 すべての Windows ランタイム (WinRT) オブジェクトと同様に、アカウントの監視は、カウントされた参照です。 呼び出す[**開始**](https://msdn.microsoft.com/library/windows/apps/hh770604) 、参照カウントをインクリメント (**停止**デクリメントが)。 開始アカウントの監視をリリースする場合、イベントがトリガーする保持されますが、呼び出すことはできません**停止**ハンドルをリリースしました。

-   アカウントの監視オブジェクトが自動的にアプリを取得、Windows によって中断されたときに停止をアプリを再開したときに再起動することに注意してください。 アプリを呼び出した場合と同じ結果になります[**停止**](https://msdn.microsoft.com/library/windows/apps/hh770606)と[**開始**](https://msdn.microsoft.com/library/windows/apps/hh770604)とで同じイベントの結果。 停止したときに発生した、アプリで何か重大な最新の状態をこれらのイベントを使用します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム API を使用するためのベスト プラクティス](best-practices-for-using-mobile-broadband-windows-runtime-api.md)

 

 







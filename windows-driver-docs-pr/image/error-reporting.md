---
title: エラー報告
description: エラー報告
ms.assetid: 6f8c08f4-2809-4f49-9332-bbee85399404
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b46db726be28d391464b342cbe3fbc6a9f6fd15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532148"
---
# <a name="error-reporting"></a>エラー報告





すべてのメソッド、 [IWiaMiniDrv インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545027)COM HRESULT 値を返します。 メソッドが成功すると、ミニドライバー返します S\_OK とクリア デバイス エラーの値、 *plDevErrVal*パラメーターが指します。 ミニドライバーが標準 COM エラー コードを返すメソッドが失敗した場合、設定と\* *plDevErrVal*デバイス固有のエラー コードを使用します。 WIA サービスを呼び出すことができます、 [ **IWiaMiniDrv::drvGetDeviceErrorStr** ](https://msdn.microsoft.com/library/windows/hardware/ff543982)によって示される値に関連付けられているエラー メッセージ文字列を取得するメソッド*plDevErrVal*します。 COM エラー値の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 





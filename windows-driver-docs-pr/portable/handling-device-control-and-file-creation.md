---
Description: Handling Device Control and File Creation
title: デバイスの制御とファイルの作成の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa6dc7786e023435495483e88e004742c9c27144
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560395"
---
# <a name="handling-device-control-and-file-creation"></a>デバイスの制御とファイルの作成の処理


Windows ベースのアプリケーションを呼び出すたびに、 **DeviceIoControl**メソッドのいずれかを呼び出して Win32 関数では、ユーザー モード ドライバー フレームワーク (UMDF) の通知、ドライバー、 **IQueueCallbackDeviceIlControl**インターフェイス。 Windows ベースのアプリケーションを呼び出すたびに、 **CreateFile** Win32 関数では、UMDF ドライバーに通知、メソッドを呼び出すことによって、 **IQueueCallbackCreate**インターフェイス。 この機能はすべてが、サンプル ドライバーの*Queue.cpp*と*Queue.h*モジュール。

次の表では、これらのモジュールに含まれるメソッドについて説明します。

| メソッド                                               | 説明                                                                                                   |
|------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| **IObjectCleanup::OnCleanup**                        | によって割り当てられたクライアント コンテキスト マップへの参照を解放**OnCreateFile** WDF ファイル オブジェクト。 |
| **IQueueCallbackCreate::OnCreateFile**               | アプリケーションが、Win32 呼び出しの結果としてデバイスを開きます**CreateFile**関数。                  |
| **IQueueCallbackDeviceIoControl::OnDeviceIoControl** | アプリケーションが呼び出しの結果としてデバイスの操作を実行、 **DeviceIOControl**関数。        |

 

参照してください、 [UMDF](https://go.microsoft.com/fwlink/p/?linkid=153678)各インターフェイスとそのメソッドの説明のドキュメント。

 

 





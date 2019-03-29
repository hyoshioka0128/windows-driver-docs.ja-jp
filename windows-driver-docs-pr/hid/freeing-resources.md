---
title: リソースを解放する
description: ユーザー モード アプリケーションと HID クライアントであるカーネル モード ドライバーは、不要になったリソースを解放常にする必要があります。
ms.assetid: 19cbc443-cc25-448f-92dc-d9586c1fd5a7
keywords:
- WDK を非表示に無料のリソース コレクション
- HID コレクション WDK、無料のリソース
- HID のリソースの解放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4cd26f4b348619b7d200bf9b47eec7b12787d8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577754"
---
# <a name="freeing-resources"></a>リソースを解放する


ユーザー モード アプリケーションと HID クライアントであるカーネル モード ドライバーは、不要になったリソースを解放常にする必要があります。




たとえば、ユーザー モード アプリケーションを呼び出す必要があります[ **SetupDiDestroyDeviceInfoList** ](https://msdn.microsoft.com/library/windows/hardware/ff550996)から取得したデバイスの一覧を識別するハンドルで[ **SetupDiGetClassDevs**](https://msdn.microsoft.com/library/windows/hardware/ff551069) HIDClass デバイスの初期化と接続操作を完了します。 呼び出しに失敗する**SetupDiDestroyDeviceInfoList**のためメモリ リークが発生します。

 

 





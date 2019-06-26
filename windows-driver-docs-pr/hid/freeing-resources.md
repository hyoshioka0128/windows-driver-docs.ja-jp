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
ms.openlocfilehash: fff45294ae04a7bd055e55e9924aacb7b6d4a15e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381782"
---
# <a name="freeing-resources"></a>リソースを解放する


ユーザー モード アプリケーションと HID クライアントであるカーネル モード ドライバーは、不要になったリソースを解放常にする必要があります。




たとえば、ユーザー モード アプリケーションを呼び出す必要があります[ **SetupDiDestroyDeviceInfoList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist)から取得したデバイスの一覧を識別するハンドルで[ **SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw) HIDClass デバイスの初期化と接続操作を完了します。 呼び出しに失敗する**SetupDiDestroyDeviceInfoList**のためメモリ リークが発生します。

 

 





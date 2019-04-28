---
title: WMI のアーキテクチャ
description: WMI のアーキテクチャ
ms.assetid: cdc8f318-1931-426e-bd9c-da7aa6a11036
keywords:
- WMI の WDK カーネルのアーキテクチャ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78d025215e6de0ee64f6c527ed476df32696e5e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379370"
---
# <a name="wmi-architecture"></a>WMI のアーキテクチャ





WMI をサポートするには、ドライバーは、WMI プロバイダとして登録します。 WMI プロバイダーは、Win32 ダイナミック リンク ライブラリ (DLL) WMI を処理する要求し、WMI インストルメンテーション データを提供します。 参照してください[WMI データ プロバイダーとして登録する](registering-as-a-wmi-data-provider.md)にドライバーが WMI プロバイダーとして登録する方法について説明します。

ドライバーが WMI プロバイダーとして登録されると、WMI コンシューマーはデータを要求し、またはプロバイダーによって公開されるメソッドを呼び出します。

WMI のカーネル モード サービスをさらに、ドライバーに IRP の要求を送信するまでのユーザー モードのコンシューマーからのクエリ要求の移動。

たとえば、WMI クライアントが指定されたデータ ブロックを要求すると WMI のカーネル コンポーネントは、ドライバーを取得または設定データをクエリ要求を送信します。 」の説明に従って、ドライバーが WMI 要求を処理[WMI 要求の処理](handling-wmi-requests.md)します。

次の図は、このデータ フローを示しています。

![wmi アーキテクチャのデータ フローを示す図](images/wmi1a.png)

 

 





---
title: フレームワーク ドライバー オブジェクト
description: フレームワーク ドライバー オブジェクト
ms.assetid: 6e9e568c-7e4f-48bd-b351-4be0e12cc15b
keywords:
- UMDF オブジェクト WDK、ドライバー オブジェクト
- framework オブジェクト WDK UMDF、ドライバー オブジェクト
- WDK UMDF ドライバーのオブジェクト
- IWDFDriver
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c9a5f69d1cefcf9c61f657fd3d6af14f9ab3c7e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368665"
---
# <a name="framework-driver-object"></a>フレームワーク ドライバー オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーによってフレームワーク ドライバー オブジェクトが公開されている、 [IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)インターフェイス。 ドライバーのホスト プロセスで読み込まれるドライバー イメージの framework 表現することをお勧めします。 フレームワークは、ドライバーのホスト プロセスに読み込まれた各ドライバーの新しいドライバー オブジェクトを作成します。 **IWDFDriver**インターフェイスは、ドライバーに渡される、 [ **IDriverEntry::OnInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-oninitialize)メソッドで、ユーザー モード ドライバーのメイン エントリ ポイントです。

 

 






---
title: デバイスにデータをアップロードします。
description: デバイスにデータをアップロードします。
ms.assetid: 50fc5f56-3758-4151-9748-dd88544006f1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c4360ef2d67d65fb65d7cc23399b63cee95fb8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550474"
---
# <a name="uploading-data-to-a-device"></a>デバイスにデータをアップロードします。


アプリケーションをデバイスからデータを転送するに使用する必要があります、 **IWiaTransfer::Upload**メソッド。 アプリケーションでは、コピー先ではなく、データ ソースとして使用されるデータ ストリームを提供します。 同様に、ドライバーの呼び出し **:read**の代わりに**IStream::Write**アップロードの状況でします。

既に存在するアイテムでのみこのアップロードの手順を実行できることに注意してください。 この手順を完了できないことをまだそのファイルを表す項目がないために、アプリケーションが storage では、デバイスに新しいファイルをアップロードしようとします。

デバイス ストレージ上の新しいファイルなど、デバイスの新しいコンテンツを作成するには、と、アプリケーションが必要です。

1.  WIA 項目を呼び出すことによって作成**IWiaItem2::CreateChildItem**項目の親となるフォルダーにします。

2.  呼び出す**QueryInterface**の**IWiaTransfer**を呼び出して**IWiaTransfer::Upload**します。

ドライバーはへの呼び出しを処理する必要があります**IWiaTransfer::Upload**それに応じて。 たとえば、WIA 項目が新しい項目の場合は、ドライバーする必要がありますファイルを作成し、で提供されているソース ストリームの内容を保存**IWiaTransfer::Upload**デバイス ストレージにします。

**IWiaTransfer**、 **IWiaItem2**、 **IwiaDataTransfer**、および**IStream**インターフェイスは、Microsoft Windows SDK の説明ドキュメントです。

このセクションの内容:

[アップロード時にドライバーの動作](driver-behavior-on-upload.md)

 

 





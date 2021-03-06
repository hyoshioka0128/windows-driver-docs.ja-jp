---
title: オブジェクト ディレクトリ
description: オブジェクト ディレクトリ
ms.assetid: b0e0d077-6736-4a54-b1eb-a30962442942
keywords:
- オブジェクトのディレクトリの WDK カーネル
- 名前付きオブジェクトの WDK カーネル
- WDK のオブジェクトのディレクトリ
- 最上位レベルのオブジェクトのディレクトリの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28fe256e7ea82465e2d1e3f111483654b1d715c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365386"
---
# <a name="object-directories"></a>オブジェクト ディレクトリ





*オブジェクト ディレクトリ*他を格納するためだけに使用される名前付きオブジェクトという名前がオブジェクト。 たとえば、 **\\デバイス**オブジェクトのディレクトリには、ドライバーによって作成された名前付きのデバイス オブジェクトが含まれています。

オブジェクトのディレクトリのファイル システム ディレクトリとを混同しないでください。 オブジェクトのディレクトリでは、オブジェクト マネージャー内でのみ存在し、ディスク上の任意のディレクトリに対応していません。 (ファイル システム ディレクトリ、実際には、オブジェクトとして表されるファイルです。)

ドライバーを作成したりを使用してオブジェクトを含む最上位レベルのオブジェクトのディレクトリの一覧を次には。

-   **\\コールバック**

    システムでは、このディレクトリに標準的なコールバック オブジェクトを作成します。 詳細については、次を参照してください。[ベンダーのコールバック オブジェクトを使用して](using-a-system-defined-callback-object.md)します。

-   **\\デバイス**

    ドライバーは、このディレクトリの名前付きのデバイス オブジェクトを作成します。 詳細については、次を参照してください。[という名前のデバイス オブジェクト](named-device-objects.md)します。

-   **\\KernelObjects**

    システムでは、このディレクトリで標準的なイベント オブジェクトを作成します。 詳細については、次を参照してください。[標準イベント オブジェクト](standard-event-objects.md)します。

-   **\\\Dosdevices\z**

    このディレクトリは、デバイスの対応するオブジェクトへのシンボリック リンクとして、デバイスの MS-DOS デバイス名を格納します。 詳細については、次を参照してください。 [MS-DOS デバイス名](ms-dos-device-names.md)します。

システムが他の最上位レベルのディレクトリを作成しますが、システムの使用に予約されています。

ドライバーは呼び出すことによってオブジェクトの新しいディレクトリを作成することができます、 [ **ZwCreateDirectoryObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)ルーチン。

 

 




